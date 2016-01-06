# V2 API

- (accepted)

(from ORFS-139)

## Background

Feedback on usage of our API is that it's been a bit too freeform, and in particular has been missing clear schemas for resources, documentation, and validation functions. In addressing these issues, utilizing swagger (which we generate today, but don't have deeper integrated) seems like it will give us a lot of these explicit wins and help us formalize a V2 interface to RackHD.

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

* Split northbound & southbound API's so they can be bound to individual interfaces and ports.
* Provide ODATA query string language to enable pagination/sorting and output filtering and Utilize JSON Schema for document declarations, validations, etc.  This gives us the technology to support Redfish style northbound API's later.
* Provide API/Schema versioning.
* Remove or limit the amount of end points with dynamic schemas as it hampers client implementations (particularly statically typed languages) and requires special case code to be written to handle outputs.
* Provided a standardized error format for JSON responses.
* Continue to provide Swagger support for client binding generation.  This will be improved a lot by removing dynamic schemas.
* Provide API security for the northbound API.  Probably read/write initially but full role based access might be appropriate.
* Provide workflow state transition API for southbound clients as an optional mechanism to events.  We can only rely on events at this point and cannot program external code to notify about task status or errors.
* Provide a single access point to update credentials for OBM/Polling (IPMI, probably applies elsewhere).
* Provide an atomic reservation system for managed resources to enable orchestration scenarios (this could be done above RackHD and could use some more thought).

As an example of northbound/southbound API separation consider we have a profiles API which both handles the CRUD for profiles but also rendering of profiles.  The northbound API could take on the role of CRUD management while the southbound API would be used exclusively for rendering to clients.  Some examples below:

    Northbound
        /profiles - GET/POST
        /profiles/:id - GET/DELETE/PATCH/PUT
    Southbound
        /profiles - GET (redirect)
        /profiles/:id - GET (rendered)

This applies to other resources like workflows which could be managed in a CRUD fashion from the northbound interface while providing tasks and a client view from the southbound.

    Northbound
        /workflows - GET/POST
        /workflows/:id - GET (maybe no reason to update/delete these resources)
    Southbound
        /workflows/:id - PATCH/PUT (possibly use this as a mechanism to transition)
        /workflows/:id/<action> (another possible way to transition)

Essentially the northbound API should be thought of as a CRUD style entry point to manage the system while the southbound API should be thought of more as the automation API for managed resources.  There may be some overlap in functionality so some route implementations may be accessible on both API interfaces.

Dynamic schemas are fairly commmon in the current API.  When using a dynamic language to consume them they don't seem very problematic but once using a statically typed language the deficiencies are more obvious.  Generally speaking it's probably better to have everything specified with well known schemas.  This could be a bit of a hassle when designing API's and documents for dynamic elements like out of band management configuration.  Some examples below:

    * Catalogs - These are truly dynamic and very difficult to model in a static language.  A unified catalog might alleviate this problem while raw catalogs could be retained or requested as needed.  It would also aid consumption from higher order services.
    * SKUs - The SKU rules are modeled in a way in which a property (dynamically) defines the operation for which to compare a field to a value.  The operation should be a field with a value that defines the operation to make the schema less dynamic.
    * Nodes - The Node document has the dynamic OBM settings field which is difficult to model.  This is a harder problem to solve but good to highlight.
    * Workflows - When creating workflows the options are varied to a degree in which modeling them is difficult.  The return values of workflows are also very dynamic and there is manual correlation to do between running a workflow, checking the active workflow end point, and then verifying it again later on the regular CRUD end point.

