# Discover and create network to compute node topology

## Background

Related to the work list in [V2 API](v2_api_with_swagger.md) in it's notion of
enabling relationships, we have sufficient information with the existing LLDP
catalog and the capability of getting related switch port information (the
mac-address/switch port table from the switch) from a remote catalog there. With
the combined information, we should be able to process those information sources
and create the relevant "links" to represent a topology from the RackHD APIs
that show what compute servers are connected to what switches, and at which port.

## Goals

* a mechanism that will capture needed data from a top-of-rack switch and combine
  it with lldp catalogs or node data where available to create or amend the
  underlying data to expose the topology connections.
* To be able to unplug one of those physical cables and have this mechanism
  update the topology correctly
* To be able to plug in a physical cable adding a second, independent network
  connection between compute node and switch, and have that connection be
  represented in the topology
* REST resource API outputs with the V2 API that show the linkages using the
  relationship structure pattern defined in V2 API
* Defined/documented events on the AMQP bus that get sent when a topology is
  calculated and a change is detected. Specifically, an event if a new link is
  formed with the details of that link, and a event if a link is broken that
  previously existed.

## API
