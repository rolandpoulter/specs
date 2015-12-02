# Workflow Task Annotation and Doc generation

(from ORFS-138)

## Background

Watching the flow of ODR-353 from the defect review this morning as it's going forward, it's clear that we're a little sub-par on our documentation of tasks provided by RackHD and "how to use them". This may equally apply to graphs, as they can be used as subelements as well.

We should develop/enable some sort of annotation onto the tasks and jobs and do something to generate documentation from that - much like how JSDocs or swagger does self-documentation of javascript functions or APIs. The benefit of keeping the documentation close to the implementation so that they don't diverge (and can be reviewed together easily), but that does the beg the question of how we present this information. Additionally, if it's annotated into the tasks, then it could conceivably be used in a UI like the workflow editor.


## Goals

- enable some mechanism that can be used to generate html based documentation that documents how to use tasks that can be found in the RackHD system
- include this mechanism within RackHD to dynamically generate relevant documentation from the tasks and graphs loaded into a running system (that is, using the data in the database)
- enable this mechanism in the build process to generate a static HTML page with documentation
- Investigate how we can expose or link this documentation to our project documentation hosted on ReadTheDocs

## API

One thing we mused about a while back as well was converting the task definitions to be json schema compliant, that way we can specify expected types, or enums of allowed values, so the UI can then present drop-down fields, better up front validation, etc. A lot of the annotations can be derived from the data structures themselves, with the rest being thrown in as tags on properties or something.
