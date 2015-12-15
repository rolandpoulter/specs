# Support DMTF SPMF for host discovery and management

(from ORFS-120)

## Background

The server industry has been traditionally using the IPMI protocol that was designed for a specific purpose of system management. However, with the industry shifting to network based programming interfaces, Restful interface architecture types such as DMTF SPMF (Redfish) have started to appear (Fall 2015) and will become more pervasive in 2016. As such, RackHD needs to support not only the legacy protocols such as IPMI, but also new Restful interfaces such as DMTF SPMF.

RackHD should support interrogating a remote machine with a standardized RedFish 1.0 specification and creating the relevant compute node and catalogs.

## Goals

- create a client within RackHD to communicate via southbound interfaces to a node using DMTF SPMF (RedFish) 1.0
 - Support "discovery" of those systems knowing the SPMF addresses given an IP address and relevant credentials
 - if available, support SSDP based discovery with configurable default credentials
- Build up and maintain relevant catalogs based on the SPMF spec
- capture SPMF based alert notifications and process those as telemetry
- support redfish/spmf 1.0 as an out-of-band interface for
 - power on, power off, recycle
 - identify on/off

## API

## Discussion

@yyscamper:

> Is there any server that has used the Redfish/SPMF interfaces, so we can have a try?
 Revert

@heckj:

> @yyscamper right now, no - looking for some samples, but we'll likely be working against "spec" for this, or maybe from simulator work depending on timing on when we start to tackle this. IDIC will be doing something here, but still somewhat TBD. Consider this strategic effort
