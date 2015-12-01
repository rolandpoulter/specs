# Queue footprint reduction

(from ORFS-141)

## Background

Following the work for establishing a footprint benchmark for a running RackHD system, there's the work to actually reduce the footprint of RackHD for a constrained system.

Anecdotal evidence from early prototype runs of RackHD in a switch indicate that RabbitMQ consumes a large portion of the resources on that system, and that it could make
sense to make RabbitMQ a configuration option and enable an alternative, lighter-weight technology for a more constrained environment.


## Goals

- determine if a ZeroMQ based queue mechanism would be footprint reduction in overall memory usage
- identify alternative queue libraries for IPC, how closely bound are we to exchange semantics?
  - can we replace it with something like ZeroMQ
- make an initial implementation to make “messenger” configurable  - either RabbitMQ or ZeroMQ backend
- try out zeromq if we think it can work, report on the footprint win (if any)

## API
