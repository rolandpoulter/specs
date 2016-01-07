# Dell R630/C6320 server level 2 support


## Background

Some RackHD basic functionality support has been verified on DELL R630/C6320 servers in functional spec "initial DELL SKU support", for example, discovery/catalog/ESXi and RHEL bootstrap. There are more features provided in RackHD to support a generic server. So we need to support more feature set (level 2) for specific DELL servers as well as exploring new feature if possible.


## Goals

- Validation of firmware tooling and support firmware upgrade (BIOS/BMC(iDrac)) with RackHD workflow
- Investigate iDrac feature set and iDrac based tooling to find out opportunities to extend RackHD capability
- Create workflow in RackHD to support identified valuable features


## API