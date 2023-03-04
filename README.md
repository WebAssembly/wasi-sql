# `wasi-sql`

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI) API.

### Current Phase

`wasi-messaging` is currently in [Phase 1](https://github.com/WebAssembly/WASI/blob/main/Proposals.md#phase-1---feature-proposal-cg).

### Champions

- [Dan Chiarlone](https://github.com/danbugs)
- [David Justice](https://github.com/devigned)
- [Jiaxiao Zhou](https://github.com/Mossaka)

### Phase 4 Advancement Criteria

`wasi-sql` should have at least two implementations (i.e., from service providers, and or cloud providers), and, at the very minimum, pass the testsuite for Windows, Linux, and MacOS.

## Table of Contents

- [Introduction](#introduction)
- [Goals [or Motivating Use Cases, or Scenarios]](#goals-or-motivating-use-cases-or-scenarios)
- [Non-goals](#non-goals)

### Introduction

The `wasi-sql` interface allows WebAssembly programs to interact with SQL databases in a generic and safe way. It provides functions for querying and modifying data, using prepared statements and handling errors. The interface is flexible and consistent, supporting various SQL flavors.

### Goals

The `wasi-sql` interface aims to provide a consistent and easy-to-use way for WebAssembly programs to access and manipulate data stored in SQL databases. It targets the features commonly used by 80% of user applications. By focusing on commonly used features, the interface aims to provide a simple and reliable way to build stateful services that access SQL databases.

The `wasi-sql` interface abstracts away specific SQL flavors and database APIs, allowing WebAssembly programs to be portable across different SQL databases that support the interface. It also abstracts away the network stack, allowing WebAssembly programs to access SQL databases without worrying about the specific network protocol used. This allows users to focus on building their applications, rather than communication details with the database.

### Non-goals

- The `wasi-sql` interface does not aim to provide support for every possible feature of SQL databases. Instead, it focuses on the features that are commonly used by 80% of user applications.
- The `wasi-sql` interface does not aim to provide support for specific database APIs or network protocols. It abstracts away these implementation details to allow WebAssembly programs to be portable across different SQL databases that support the interface.
- The `wasi-sql` interface does not aim to address control-plane behavior or functionality, such as cluster management, monitoring, data consistency, replication, or sharding. These are provider-specific and are not specified by the wasi-sql interface.

### API walk-through

For a full API walk-through, see [wasi-sql-demo](https://github.com/danbugs/wasi-sql-demo).

> Note: This README needs to be expanded to cover a number of additional fields suggested in the
[WASI Proposal template](https://github.com/WebAssembly/wasi-proposal-template).