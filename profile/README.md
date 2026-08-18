# ReifyDB

**The database that runs your backend logic.**

One database instead of Postgres + Redis + a queue + a cron job.

## What it is

ReifyDB is one database for live application state: the balances, positions, sessions, workflow steps, counters, and derived numbers your application reads and writes on every request.

- **Tables** hold the rows. State lives in memory and is persisted asynchronously, off the hot path.
- **Views** hold the derived numbers, and the write keeps them current. Nothing to refresh, nothing to poll.
- **Transitions** run your rules inside the transaction that changes the data. They are procedures and handlers: code you version and test inside the database, not a trigger someone forgot.
- **Primitives** are built in: counters, queues, ring buffers, histograms, all under the same transaction.
- **It knows who is asking.** Clients talk to ReifyDB directly over WebSocket or HTTP and authenticate as themselves. Policies decide, per user, what may be read and written. No shared service account, no privileged connection to hijack: a hostile query runs as the user and can do nothing the user could not do anyway.
- **Embedded or server.** Inside your process like SQLite, or standalone.

## What it replaces

| You run today | With ReifyDB |
|---|---|
| Postgres + Redis | one transactional store, in memory, persisted asynchronously |
| Batch materialized views, cron | incremental views, current on write |
| Workers, queues, logic scattered across services | transitions inside the transaction |
| Redis + Kafka + custom code for counters and queues | native state primitives |
| One shared database password, rules re-checked in every service | per-user auth and policies at the data |

## What it is built on

1. Derived state is the database's job.
2. A rule enforced in a service is a rule enforced sometimes.
3. One write, one truth.
4. Counters, queues, and buffers are state, not cache.
5. The network is the speed limit.
6. The application user is the database user.

## What it is not

Not a BI warehouse and not an analytics engine for ad-hoc queries over cold history. Those belong in different systems.

## Status

Version 0.9. Not production ready. APIs and guarantees will change. Apache-2.0.

[reifydb.com](https://reifydb.com) · [manifesto](https://reifydb.com/manifesto) · [docs](https://reifydb.com/docs) · [github.com/reifydb/reifydb](https://github.com/reifydb/reifydb)
