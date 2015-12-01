# UEFI Workflow Support

(from ORFS-69)

## Background

Currently OnRack only supports BIOS Legacy mode, there needs to be support for UEFI only mode.


## Goals

- Allow nodes to load and boot into iPXE while configured for UEFI mode.
- As part of a workflow, capable of booting various UEFI applications for running extended diagnostics or UEFI firmware upgrade utilities.

Success Criteria

| num | goal | details |
|-----| -----| --------|
| 1	| Detect architecture mode during DHCP process.	| Update OnRack DHCP configuration to check architecture type code (option 93) for legacy or UEFI mode, and provide corresponding image per type (EFI32, EFI64 or legacy). |
| 2| Network boot microkernel overlay image. | PXE boot microkernel discovery image in UEFI mode using EFI enabled iPXE image (either 32 or 64 bit image). |
| 3	| Network boot UEFI firmware update utilities. | PXE boot UEFI utility as part of workflow to execute firmware updates through UEFI. |
| 4	| Network boot UEFI extended diagnostic utilities. | PXE boot UEFI extended diagnostic utilities as part of workflow (i.e. extended POST utility) |
| 5	| Compatibility between modes. | Maintain compatibility between Legacy and UEFI modes.
* We want to be able to move back and forth between legacy and UEFI boot profiles
* Want to boot UEFI and bootstrap an OS
* Then switch to legacy boot and bootstrap an OS
* Then back to a UEFI mode and bootstrap an OS

## API
