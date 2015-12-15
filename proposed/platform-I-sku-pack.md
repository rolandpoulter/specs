# Secure erase workflow task

(from ORFS-133)

## Background

EMC has an internal Intel based platform that we want to verify (Platform-I)
to support internal hardware sharing projects with automated re-provisioning
and integration into internal testing and validation frameworks. In order to
support that, we want to make sure our tooling functions to discovery this
platform and that our default workflows function for base OS installation.

With the addition of the concept of [SKU packs](../in-progress/sku_packs.md) we
want to create package any workflows, profiles, templates, microkernels, and SKU
definition stanza's in that format if needed in addition to defaults or
existing reference workflows, etc.

## Goals

 - Discovery:
   - product name
   - part number
   - serial number
   - macaddress of all nics
   - CPU count, speed
   - DIMM count, genealogy
- OS installation
   - CentOS/RHEL
   - ESXi 6.0

## API
