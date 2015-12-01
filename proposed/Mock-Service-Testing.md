# Mock Service Testing

1. Background
  * In an effort to decrease drag and to implement fast integration testing for RackHD it has come to light that we need a testing framework that will allow us to effectively exercise our services and emulate common environments without the need for virtual or physical hardware. We intend to create tools to emulate the behavior of live systems, and interact with our services in order test the functionality of the code in a reproducible and deterministic way. 
  
2. Goals
  * Main scope:
    * Boot Traffic - DHCP requests
    * TFTP requests
    * HTTP requests from iPXE
    * HTTP requests from the initrd and linux microkernel environments
  * Workflow Testing
    * Run Bootstrap.js in test
    * Mock Catalog commands
    * Mock Flash commands
  * Nice to have.
    * Switch/PDU mocking
    * SNMP endpoints
    * Mock IPMI endpoints  

  a) Implement config framework (node)  
  b) Implement mocks/emulators (bash / node / [python?] )  
  
3. API
  * If there are REST or other APIs involved in this functionality, start to flesh them out here
  
  
