# SKU Packs

- (accepted)

## Background

Feedback from users indicated:
* The need to override default functionality with SKU specific functionality.  
* The need to dynamically load SKU specific content without having to bundle it with RackHD.

## Goals

* Provide a method within RackHD to override default functionality with SKU specific functionality.  

    > @heckj: Can we call out that we want a specific REST API as that method?

* Provide a method within RackHD to dynamically load SKU specific content without having to bundle it with RackHD.
* Documenting the SKU pack format and any manifests associated with it
* Provide at least 1, if not a couple, of SKU packs
* Create light (developer oriented notes) documentation on how to assemble a SKU pack and add it to the RackHD user's guide (in ttps://github.com/RackHD/docs/tree/master/docs/rackhd)
* Update the demo in https://github.com/RackHD/RackHD/tree/master/example to use a SKU pack instead of the piecemeal stuff we provide for Auto-install setup of CoreOS for virtualbox


## API

## Discussion

@heckj:

> made ORFS-154 to keep to our internal tracking

--------

@heckj:

> Please add goals for
> - documenting the SKU pack format and any manifests associated with it
> - provide at least 1, if not a couple, of SKU packs
> - create light (developer oriented notes) documentation on how to assemble a SKU pack and add it to the RackHD user's guide (in https://github.com/RackHD/docs/tree/master/docs/rackhd)
> - update the demo in https://github.com/RackHD/RackHD/tree/master/example to use a SKU pack instead of the piecemeal stuff we provide for Auto-install setup of CoreOS for virtualbox

@heckj:

> Question: is the intention that loading a SKU pack is persistent to the instance of RackHD, or ephemeral? I.e. if you upload a SKU pack and reboot the whole system, should the data be retained and auto-reloaded when the system comes back up?

@zyoung51:

> The first crack at it has the SKU pack coupled to the _id of the sku in MongoDB. An HTTP POST would associate the sku pack tarball with a particular sku (ie: POST /api/common/sku/:id/package) and would ultimately place it onto the filesystem to persist.

@heckj:

> Cool - persistence makes a lot of sense, was hoping that's where you were heading

----------

@yyscamper:

> @amymullins : Please correct me if my understanding is not correct.
> SKU pack is something like plugin-in, it will define all SKU specified features. For example, for SKU-0, it should send command-0 to light the system LED; but for SKU-1, it should send command-1 to light the system LED.

> If feed this pack into RackHD code architecture, hardware specified function will work well.

> So first we need to find a way how to define the SKU specified function. Then improve the RackHD architecture to support such plugin-in mechanism.
