---
title: "Active Objects"
date: 2021-02-11
tags: [development]
publish: true
---

# Active Objects
In concurrent system exposing objects methods can create lot of synchronization
and thread safety issues. Active object pattern provide way to protect
object state in concurrent system. Instead of exposing objects methods directly
to client communication happens through well defined structured messages.

Usually we will have one thread per active objects with its own message receive 
queue. Due to serialize operation on event processing avoid mutual execution 
becomes much simpler.

Each active object communicate with each other using message or event queue.
Results of operation executed by server active object will be communicated 
using message or event queue.

# Advantages 
Instead of protecting individual objects under thread with mutex per object,
active object provide serial access using queued message handling. Which provide
simpler approach to avoid race conditions.

# Disadvantages
As communication is asynchronous between active objects there may additional 
synchronization efforts required if we want to synchronize reply. Client
active object must maintain state till it get reply and transaction is complete.

For every encapsulated object a message structured needs to be define. We can
avoid this by making sure only state less objects can expose methods or services
to client directly.

# Messaging
As active objects communicate/calls operation indirectly using messages. Object
method execution and parameter passing is done by enclosing these parameters
in messages. Similarly return values are communicating using message reply.


# Implementation
In RTOS task with message queue exposing communication messages struct matching
with expected method parameters can be implemented using task and message queue
per task.

# A note on Command pattern
This pattern is similar to command pattern which generally provide synchronous 
execution of command.
