# In-band management/workflow support

(from ORFS-143)

## Background

Extending the concepts of workflow orchestration to have more knowledge and (potential) access to systems after the OS has been laid down means extending in a number of new ways. Knowing about network configurations and connections, access via SSH to the host OS, and the potential to grab significant and additional telemetry or install additional packages. The first steps to this are to enable SSH access to a HOST OS and to reflect similar information in our data models/API resources


## Goals

- add representation and appropriate schema for nics and networks to compute nodes, switches
- add representation of an IP address and credentials to inquire for OS level details
  - expand catalogs to include package collection, versions
  - expand workflow tasks to arbitrary SSH commands with credentials from node
       (https://github.com/mscdex/ssh2, https://github.com/tsmith/node-control, https://github.com/mikeal/sequest
  - expand catalogs to include a network connection catalog - nics, IP
  - enable IP lookups to link data flow from compute servers into pollers/statsd ingest

## API
