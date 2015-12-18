# Workflow support leveraging RACADM

(from ORFS-146)

## Background

Dell servers with newer versions of iDrac (v7, 8) support BIOS configuration manipulation through the linux CLI tool RACADM. Create support for workflow tasks that leverage this tooling to enable workflow/hardware orchestration flows to utilize this technology.


## Goals

- create workflow task that leverages RACADM through a microkernel
- create documentation and an OEM flow to create that microkernel
- investigate using RACADM remotely as a workflow task as well
- review RACADM command set available in v7 and v8 and propose catalogs to be captured that we don't get in other fashions today
- create dell specific discovery workflow that uses this information to capture additional detail about Dell servers

## API
