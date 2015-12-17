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

### Research Notes

MQTT

 - http://mcollina.github.io/mqtt_and_nodejs/
 - http://www.mosca.io

## Discussion

@heckj:

> @jlongever I think mentioned MQTT, and while doing some weekend reading I stumbled across some articles on MQTT and NodeJS, including some effusive praise for the "mosca" library, so wanted to scribble that in here for future reference and reading

@benbp: 

> @heckj it was @zyoung51 who brought up MQTT.

@zyoung51:

> @heckj, @benbp What is your plan for topic discussion?

> The discussion I had with Ben was regarding using Mosquitto (http://mosquitto.org/) and writing my own C program with minimal dependencies to create an embedded task runner for the discovery image. The workflow author would understand that nodeid-domain based task runners will only accept shell command/downloadUrl tasks, which would make the c program simpler (dumber). In that case, the scheduler RabbitMQ would talk to the nodeid-domain using MQTT (https://www.rabbitmq.com/mqtt.html). I wrote some code to do it, but didn't like how the MQTT adapter in RabbitMQ was bound to a single exchange for all MQTT topics.

> I've used Mosquitto before, which is why I thought of it first, but the RabbitMQ C binding would probably make more sense (https://github.com/alanxz/rabbitmq-c) for an embedded client.

@heckj:

> I just happened to run across the presentations this past week on MQTT and a Node.js library, and that Ben had mentioned some earlier conversations with you, but I didn’t know the details, so tacked in the references in case they were useful.

> What to actually do and which libraries to use I’ll defer to you guys for what gives us the functionality we need/require but possibly has a lighter footprint than running a full AMQP server for the scenario of running inside a top-of-rack switch
