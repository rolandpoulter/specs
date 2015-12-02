# Add HTTP proxy functionality

(from ORFS-125)

## Background

In order to provide a minimal deployment for development and demonstration environments it would be nice to support HTTP proxy configuration that would be compatible with the existing repository system for workflows.  OS installation repositories are large and making it easy to configure a repository with HTTP proxy will reduce the need to download the entire repo for some usage scenarios.


## Goals

- Support HTTP proxy configuration via monorail.json.
- Update on-http to mount HTTP paths with appropriate forwarding to external resources based on monorail.json configuration.
- Prove that a proxy configuration can seamlessly replace one of our deployed static repositories and/or an external repository that is available on the control network.
- Allow configuration of one or more HTTP proxy paths to enable external resources to be accessed by managed nodes.
- Provide the flexibility for supporting mulitple external "repositories" (one for CentOS, one for Ubuntu, etc)
- Provide a configuration that can be changed via API that provides a mapping for external repositories to "internal mapping" for OS installation, etc.
- Ensure that existing workflows and their repository path assumptions work correctly with a proxy configuration in place.
- Favor local static files over proxy configuration to ensure proxy is a fallback.
- To support the concept of building into a caching proxy to support a local cache of files for frequently used files to reduce overall bandwidth consumption over time
- Support configuration to both HTTP and HTTPS remote proxies

*Note*: This will change the parameterization of how we specify the repository location to work with this proxy - it would no longer be necessary to point to a local internally built repository, but to one of the proxy configuration mappings so that the proxy determines where and how to find the relevant files. The proxy configuration will need to be set prior to invoking a bootstrap call with a proxy location included within it.

## API

To implement this proxy we'll need the following items:
1. A configuration setting in monorail.json that outlines the proxy path to server relationship.
1. An update to on-http to utilize the new configuration value.
1. An express middleware capable of handling the proxy requests.

Configuration Setting:

```{
    "httpProxies": [
        {
            "localPath": "/localpath",
            "server": "server.to.proxy.to.com",
            "remotePath": "/remotepath"
        }
    ]
}
```

This is an example configuration and may change some depending on the proxy configuration but the goal is simply to map some local path to an external server & path.

**Express HTTP Proxy Packages**:

https://github.com/villadora/express-http-proxy is the only package I've looked at extensively. There may be others out there but this is probably a good starting point.  I don't believe we need to concern ourselves with caching support as this is largely a development and demo feature.  A production system would want local repositories in most cases for installations though it may be reasonable to use proxy in a deployment assuming the proxied servers were co-located with the deployment.

**Routing Precedence in Express**:

In order to ensure local static files are favored over proxy the initialization of the proxies should be done after static files are mounted.
