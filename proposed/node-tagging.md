# Node Tag and Label System

## Background

Identified the need to assign labels to a node.  This would allow an Infrastructure M&O layer to manage the node by assigning or clearing labels which may trigger workflows.  Examples labels can include “quarantine”, “allocated”, “unallocated”, “provisioned”, etc…


## Goals

* Add a key for an array of labels/tags to the node model.  
* Add API to POST/DELETE labels(tags).  Depending on Infra to apply/remove tags based on HW events.
* Register workflows to be run on label/tag add and remove events.


## API
