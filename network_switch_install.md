# Network Switch zero-touch installation and discovery

(from ORFS-124)

## Background

Extending on network switch discovery that's enabled in RackHD via a REST API, add the discovery capabilities to RackHD so that an Arista switch attempting to ZTP boot/install on the network to which DHCP/TFTP is attached and listening successfully installs and a relevant node is created in the REST API. We additionally want to support installation and initial configuration of a Cisco switch using ZTD installation mechanisms (Cisco's equiv of the ZTP protocol).


## Goals

* ZTP based installation (or equiv protocol/mechanism) for an Arista switch
* ZTD based installation (or equiv protocol/mechanism) for a Cisco switch
* ONIE based installation (or equiv protocol/mechanism) for a Brocade or Celestica switch
* Initial configuration for the switch defined as a file that can be uploaded via the RackHD API
* Configurable default username and password in RackHD configuration file to be used for future SNMP read-only access to the node
* After ZTP process is complete, Node created in RackHD catalog
  * SNMP switch pollers created using appropriate credentials

## API
