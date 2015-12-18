# IPMI poller improvements

- (accepted)
(from ORFS-134)

## Background

IPMI offers two general classes of sensors: threshold and discrete.  Threshold sensors report an analog value that must fall within a specified range.  If the sensor value is outside of this range, the sensor asserts a condition indicating that the IPMI entity with which the sensor is associated is outside of its operating envelope.  Discrete SDRs report a value consisting of a set of discrete states specific to each type of sensor.

Following a conversation with EMC reliability engineering, we've determined that the components most likely to fail are power supplies and memory.  Based on this analysis, we decided that generating alerts for these components should be a priority.  Power supply and memory devices are represented by discrete SDRs which are not current supported by the RackHD IPMI poller.  The SEL will temporarily be substituted for discrete SDRs but has some some limitations:
- SEL entries do not contain sensor name string (e.g. "PSU1 Status").  Only a numeric sensor identifier is available.
- The SEL poller must be configured using an API call and thus only works in conjunction with an external entity.

This functional spec covers the work required to enhance the IPMI SDR poller to allow processing of discrete SDRs so that the SEL is not needed to generate alerts for power supply and memory devices.  An additional "nice-to-have" piece of work is to normalize the messages published by the SEL and SDR pollers so that they have the same basic structure.  This will help simplify subscriber parsing logic.

## Goals

- Use `ipmitool -v sdr` command in place of `ipmitool -c -v sdr`.
- Update ipmitool response parsing logic.
- Update SDR poller to process objects in the form shown below.
- Change SDR poller published message format (see example below).
- Change SEL poller published message format (see example below).
- Update IPMI SDR poller to handle discrete sensor state assertions
- Normalize output from SDR and SEL pollers to simplify ingestion of messages.

## API

parsed ipmitool output (poller input) example:

```
[ { sensorId: 'PSU1 Status (0xe0)',
    entityId: '10.1 (Power Supply)',
    sdrType: 'Discrete',
    sensorType: 'Power Supply (0x08)',
    sensorReading: 'ffh',
    eventMessageControl: 'Per-threshold',
    statesAsserted: [ 'Power Supply', 'Power Supply AC lost' ],
    assertionsEnabled:
        [ 'Power Supply',
         'Presence detected',
         'Failure detected',
         'Power Supply AC lost' ],
    deassertionsEnabled:
        [ 'Power Supply',
         'Presence detected',
         'Failure detected',
         'Power Supply AC lost' ],
    oem: '0'
  },
  { sensorId: 'PSU2 Status (0xe1)',
    entityId: '10.2 (Power Supply)',
    sdrType: 'Discrete',
    sensorType: 'Power Supply (0x08)',
    sensorReading: '0h',
    eventMessageControl: 'Per-threshold',
    assertionsEnabled:
        [ 'Power Supply',
          'Presence detected',
          'Failure detected',
          'Power Supply AC lost' ],
    deassertionsEnabled:
        [ 'Power Supply',
          'Presence detected',
          'Failure detected',
          'Power Supply AC lost' ],
    oem: '0'
  }
]
```
