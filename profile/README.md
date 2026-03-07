# ReifyDB – Application State Database

## About ReifyDB

ReifyDB is a **database designed to manage application state**.

It stores, mutates, and derives live application state under a single transactional model.  
State is kept in memory for low latency, persisted asynchronously for durability, and extended with application defined logic that runs next to the data.

ReifyDB is built for systems where correctness, freshness, and predictable performance matter more than synchronous durability on every write.

---

## What ReifyDB Is For

ReifyDB is designed for **application owned state**, such as:

- User and session state  
- Trading and financial state  
- Game and simulation state  
- Workflow and process state  
- Counters, queues, buffers, and aggregates  
- Derived state that must stay correct as data changes  

It is not designed for BI, analytics warehouses, or untrusted multi tenant SQL access.

---

## Core Capabilities

- **Transactional Application State**  
  ACID transactions over live, mutable application state with predictable low latency

- **Incremental Derived State**  
  Materialized views that update automatically as state changes, without polling or batch refresh

- **Programmable State Transitions**  
  Application defined logic that runs inside the database under the same transactional guarantees

- **Multiple Native State Primitives**  
  Tables, views, counters, ring buffers, histograms, and other state structures in one engine

- **Asynchronous Durability**  
  State is persisted off the hot path with bounded durability latency and deterministic recovery

- **Direct Client Access**  
  Applications and services can connect directly using WebSocket or HTTP without intermediary APIs

---

## Design Principles

- Application state is first class  
- All state changes happen through transactions  
- Derived state is maintained incrementally  
- Logic runs next to state, not around it  
- Durability is decoupled from commit latency  
- The database is owned by the application, not end users  

---

## Philosophy

> Your application state should live in one place.

ReifyDB reduces complexity by eliminating fragmented state across databases, caches, workers, and background jobs.  
Instead of stitching together multiple systems, ReifyDB provides a single transactional engine for state, logic, and derived data.

---

## What ReifyDB Replaces

Modern applications often manage state across multiple systems. Each layer adds complexity, operational overhead, and failure modes.

ReifyDB replaces these patterns by centralizing application state under a single transactional engine.

### Databases Plus Caches

Traditional stacks separate durable storage from fast access layers.

- PostgreSQL or MySQL for persistence  
- Redis or Memcached for speed  
- Manual cache invalidation and consistency logic  

ReifyDB combines durability and low latency state access in one system. State is kept in memory for fast reads and writes and persisted asynchronously, removing the need for a separate cache layer.

---

### Batch Materialized Views and Polling

Many systems rely on background jobs to keep derived data up to date.

- Periodic refresh of materialized views  
- Polling based read models  
- Cron jobs and scheduled workers  

ReifyDB maintains derived state incrementally as part of the write path. Views stay correct automatically as data changes, without polling, refresh jobs, or batch recomputation.

---

### Glue Code and Background Workers

Application logic is often scattered across services.

- Triggers in the database  
- Workers updating counters and aggregates  
- Custom in memory state machines  

ReifyDB allows application defined state transitions to run inside the database under transactional guarantees. Logic and state evolve together, reducing glue code and synchronization bugs.

---

### Fragmented State Primitives

Different state representations are often handled by different systems.

- Tables in databases  
- Counters and queues in Redis  
- Buffers and streams in custom services  

ReifyDB provides multiple native state primitives under one transactional model. Tables, counters, ring buffers, and derived views all participate in the same consistency guarantees.

---

ReifyDB simplifies application architectures by replacing stacks of loosely coupled systems with a single, coherent model for managing application state.
