# Secure erase workflow task

(from ORFS-153)

## Background

We want to be able to wipe out data from an existing node with more surety than
just nuking the filesystem. RackHD and the microkernel that it uses needs to
have the correct tools to erase (quickly, and also securely) disks on nodes that
are under management.  Note that data in bad sectors and some data in flash
drives may not be accessible for overwriting, but may still be recoverable.
Secure erasure cannot be guaranteed due to this, but we should be able to give
this a pretty complete pass to get close.

We're aiming to provide a reasonable substitute with reasing "G-lists" and
then performing a 3 to 7 time multi-pass overwrite of addressable locations

## Goals

 - workflow that iterates through all disks available to it and performs a
   multipass wipe of the data consisting of:
   - character write
   - complement of that character write
   - random character
   - verify
 - when complete, drives should act as though they're "fresh out of the box"
   with no remnants of filesystem sectors or partitions remaining.

## API
