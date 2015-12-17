# Mock Service Unit-Testing

- (accepted)

1. Background
  * Current RackHD unit-tests rely on dependent services running to exercise core interfaces such as AMQP, MongoDB, DHCP, TFTP access. These unit-tests (i.e. on-dhcp-proxy, on-core) should be refactored to remove these dependencies and be replaced with mocked interfaces that mimic expected behaviors. This change will also help provide deterministic testing to better manipulate service behavior that helps validate the internal design logic.

2. Goals
  * Main scope - Mock out dependent services and communication protocols:
    * on-core (helper start/stop methods, mock AMQP and MongoDB interfaces)
    * on-taskgraph (service graph, registry interfaces)
    * on-dhcp-proxy (dhcp request/offer, message handler interfaces)
    * on-tftp (tftp get request interface)
    * on-http (http request interface)
    * on-tasks (ipmi and snmp command util interface)

  a) Evaluate current unit-test dependencies and helper functions  
  b) Implement new mocks (mocha/chai/sinon)

3. API
  * Mocha unit-test framework

  https://groups.google.com/forum/#!forum/rackhd
