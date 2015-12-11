# Node Tag and Label System

## Background

Identified the need to be able to assign tags to a node. This would allow an Infrastructure M&O layer to manage node(s) by running workflows as the tags are applied/cleared to all nodes with a given tag.  Examples tags can include “quarantine”, “allocated”, “unallocated”, “provisioned”, etc…  This Functional Spec captures the development efforts needed to bind event handlers (as workflows) to events (tags) and define a way for an Infrastructure M&O Layer to emit events (tags). 



## Goals

* Add a key for an array of tags to the node model.  
* Add APIs to GET/PUT/DELETE tags.  
* Register workflows to be run on tag add and remove events.



## API

PUT /nodes/:nodeid/tags - Add a tag to a node
GET /nodes/:nodeid/tags - Get a list of tags on the node
DELETE /nodes/:nodeid/tags/:name - Remove a tag from a node

POST /tags - Create a tag
GET /tags - Get a list of all tags
GET /tags/:name - Get information about a tag
GET /tags/:name/nodes - Get a list of nodes that have the tag
PUT /tags/:name - update a tag's add/remove workflows/settings
DELETE /tags/:name - Delete a tag

