# SSDP Discovery for Compute node BMCs

(from ORFS-136)

## Background

Intel and AMI based BMC's all (apparently) support and expose a service beacon using the SSDP protocol (https://en.wikipedia.org/wiki/Simple_Service_Discovery_Protocol). Right now discovery in RackHD is via two methods - 1) telling RackHD about a machine using the REST APIs to post a new node and 2) the default method of enabling RackHD to add any machine that attempts to PXE boot against as a new node, leveraging a default "discovery" workflow.


## Goals

- Investigate the specifics of what intel and AMI BMC's present via SSDP
- Enable an SSDP listener for the RackHD system that leverages this discovery mechanism to identify BMC's on a given network
- Leverage that into creating nodes for BMC's "discovered" on that network if BMC access can be verified
- Support the use of a set of possible username/password combinations in a configuration file to attempt to access the BMCs found via SSDP discovery
- Invoke a "passive discovery" process that adds catalog information to the node using BMC/IPMI only access as a default to this workflow process
- Support an option for an additional discovery workflow to be invoked that will PXE boot the relevant node for cataloging and SKU identification

## API
