# Add HTTP proxy functionality

(from ORFS-140)

## Background

We want to consider future work for reducing the resource footprint for running RackHD as a system to make it more amenable to running in a top of rack switch or other "constrained" environments. To enable that, we need clear measurements of where to make improvements and a benchmark to measure improvement against - a means of getting those and clear marker for success.


## Goals

- create repeatable benchmarks to measure memory and CPU footprint within a consistent system for a basic set of tasks (for example, maybe a 5 node discovery, installation of an OS, monitoring IPMI)
- pick 1 benchmark set (configuration, run-through, etc) as an initial baseline for footprint comparison work
- measure each process independently - CPU, memory consumed, disk IO, network IO - plot over lifetime of tasks
  - analysis should also measure mongodb and rabbitmq
- measure disk consumed in mongodb
- come up with metrics to compare each so we know where we’re consuming the most resources
- process needs to be easily repeatable with distinct metrics from each run to compare as we change over time

## API
