# V2 API

(from ORFS-139)

## Background

Feedback on usage of our API is that it's been a bit too freeform, and in particular has been missing clear schemas for resources, documentation, and validation functions. In addressing these issues, utilizing swagger (which we generate today, but don't have deeper integrated) seems like it will give us a lot of these explicit wins and help us formalize the a V2 interface to RackHD.

## Goals

API w/ swagger
 - /api/v2 running in parallel with /api/v1.1
 - integrated swagger "try it out functionality"
 - add resource validation based on schema definitions
 - figure out how to bind/specify authentication with passport
 - separate out south-bound http interactions (microkernel tasks, templates,
     profiles) from client interactions
 - support configuration to bind northbound (with authentication) onto dedicated IP address
 - support configuration to bind southbound onto dedicated (separate) IP address

API Resources
 - specify schema for the api resources
 - explicit schema for nodes (switch, compute, etc)
   - explicit schema for catalogs (aside from the internal data)
   - explicit schema for OBM settings for compute nodes
   - explicit schema for equiv OBM settings for switch nodes
   - explicit schema for relations between nodes
 - explicit schema for pollers
 - explicit schema for alerts
 - explicit schema for workflows
  - explicit schema for tasks
  - explicit schema for SKU

New resource/data model support
   - need to support storing and exposing topologies through RackHD APIs
    - explicit schema for relations between nodes
    - switch ports to compute nodes
    - PDU ports to compute nodes & switch nodes

## API
