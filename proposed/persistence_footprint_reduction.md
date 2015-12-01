# persistence footprint reduction

(from ORFS-142)

## Background

Following the work for establishing a footprint benchmark for a running RackHD system, there's the work to actually reduce the footprint of RackHD for a constrained system.

In the vein of reducing the footprint of running RackHD in a smaller environment, MongoDB consumes a significant amount of disk space and memory consumption (anecdotally anyway), and there may be a benefit in replacing MongoDB itself with a more constrained library that has similiar semantics - underneath waterline or or ORM layers in RackHD - as a configurable option.


## Goals

- determine if an alternative MongoDB like library would be footprint reduction in overall memory usage
- can we replace our underlying persistence through our ORM (waterline) with something that requires less system resources
- identify alternative persistence library (ben had one he was thinking about)
- make an initial implementation to attempt replacing it, configurable, and measure the overall system footprint success

## API
