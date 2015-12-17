# Workflow HA and fault tolerance

- (accepted)
(from ORFS-100)

## Background

Within the on-taskgraph graph runner, there is too much state stored in memory that is not persisted or accessible out of process (and therefore the inability to spin-up new task runners to meet demand). Graph state should be stored in the database with little to no in-memory state, such that tasks can be picked up by more than one process. This will increase the scalability, fault-tolerance, and debuggability of graphs. Additionally, general refactoring of technical debt in the graph and task projects needs to be undertaken to support the above goals.


## Goals

* TaskGraph (on-taskgraph/lib/task-graph.js) and Task (on-tasks/lib/task.js) objects should be entirely serializable and de-serializable from database-backed state, without any dependency on in-memory state.
* TaskGraph runners should be more like normal schedulers and be able to pick up Task work items that belong to any graph.
* Tasks and graph context should be stored in the database, and tasks should be able to access one or many context objects in the database.
* Task and graph data structures should be reasonably human-readable for debugging/tracing, and be size-efficient.
* Base task definitions should be merged into Job class schemas.

## API

**Terms:**

*Scheduler*

 A process that performs graph state evaluation on demand, and requests Task Runners to run a task. Any number can run in coordination.

*Task Runner*

 A process that receives task run requests, and runs tasks, then persists and alerts task state when finished. Any number can run in coordination.

Key directives:

- Entirely database backed: no workflow state kept in memory.
- Stream based architecture (Reactive paradigm): The Scheduler and Task Runner are just processing pipelines that responds to events. Very modular architecture which allows for flexibility in regards to the database and messaging infrastructure.
- Atomic checkout: All eligible Schedulers or Task Runners will receive requests, but only one will succeed in checking out a lease to handle that request. Somewhat like a leased queue model.
- Fault tolerant: State changes are primarily learned about via AMQP events for fast reaction times, but all state is persisted, so in the case that AMQP messages are dropped or a Scheduler/Task Runner instance goes down, there are periodic database pollers that re-send the AMQP events to remaining Schedulers/Task Runners. Additionally, any instance responsible for handling of a task must update a heartbeat Date on it in the database, so that other instances can pick up dropped work.
- High availability: Scheduler and Task Runner will be able to be be configured to handle different domains of nodes/jobs/etc. and will be machine independent as long as the database and AMQP are shared. Just run N number of processes that you need.

**Basic ideas/walkthrough:**

- A scheduler owns a group of tasks, and every time a task changes state or its DB poller tells it to, the scheduler will check for any non-running tasks that have an empty list of dependencies that need to be fulfilled before running. It then sends out an AMQP event to tell listening Task Runners to run that task.
- Only one Task Runner will succeed in checking out ownership of a task. It will then run the code associated with the task, and persist the task + send out an AMQP event when that task finishes. The receiving scheduler will also update all task documents that have the task listed as a dependency, so that when it re-evaluates the workflow graph it will know what to run next.
- All Schedulers are periodically checking for any task/task dependency documents that have expired lease heartbeats, or no lease ownership at all. This ensures that any missed events or failed processes do not result in dropped work.
- The workflow definitions will be similar to what they already are, with added support for better branching and context sharing, but they will get compiled into a data structure that is optimized for fast database queries and easy database indexing.
