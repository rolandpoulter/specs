Integration testing covers all quality gate steps plus additional developed and maintained functional tests available outside of the smoke test step.  CI should be executed continuously regardless of pending pull-requests or commit merges; once a CI cycle completes another begins.  

## Background

We need our own integration tests now that we're an independent project, basically.

## Goals

The goal of CI is to build confidence in the master branch code base quality, ensuring a fully functional state and able to be deployed at anytime.

### System Level Integration:
This level of testing covers end-to-end functionality through the integration of all external dependencies at the system level. The testing framework externally drives input exercising all integrated functional components and evaluates the expected output response.

Targets all RackHD components including their dependencies such as rabbitmq and MongoDB.  

Targets manageable node dependencies such as enclosures, compute nodes, PDU's, and switches that are accessible to the RackHD system.  These dependencies can be a mix of virtual and physical hardware or be a complete virtual rack.  The virtual rack approach provides more deterministic behavior, with integrated controls and prevents physical hardware resource constraints.

Targets end-to-end functionality controlled via external test framework (considering Python proboscis).

As a work proposal, considering devstack as an inspiration, integration test structure will look like:

- Setup/deployment scripts (leveraging our existing vagrant/virtualbox setup for virtualized test environments, and a mix of new and existing scripts
for physical test environments)
- Tests are driven by python frameworks, considering a combination of nose+proboscis. Python mainly chosen because a lot of the environmental modifications
necessary for different tests are likely to be a mix of shell glue and code, which Python seems the best fit for.
- We are anticipating that tests themselves will mainly take the form of black box API tests, plus a mix of OBM calls and database/AMQP calls to set up test state.

### Isolated Integration:

This enables a psuedo style integration test that exercises RackHD components in isolation against their external services such as rabbitmq or MongoDB.  This test level targets development environments and external CI platforms such as Travis-CI that cannot access external nodes.  Input/Output is driven using unit-test style mock frameworks.

### Running

While it would be convenient to run tests in travis-ci, only a small subset of meaningful tests are really able to be run there. At a certain point, it makes more
sense to use real or virtual nodes in the test environment. The proposal is that testing will take the form of internal systems posting out to github for
tests we deem need to be PR gates, and also that the virtualized integration test environment should be relatively low-resource and easy to set up, such
that internal and external developers can exercise integration tests against their code with little difficulty.
