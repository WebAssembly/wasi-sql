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
- [API walk-through](#api-walk-through)
  - [Use case 1](#use-case-1)
  - [Use case 2](#use-case-2)
- [Detailed design discussion](#detailed-design-discussion)
  - [[Tricky design choice 1]](#tricky-design-choice-1)
  - [[Tricky design choice 2]](#tricky-design-choice-2)
- [Considered alternatives](#considered-alternatives)
  - [[Alternative 1]](#alternative-1)
  - [[Alternative 2]](#alternative-2)
- [Stakeholder Interest & Feedback](#stakeholder-interest--feedback)
- [References & acknowledgements](#references--acknowledgements)

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

[Walk through of how someone would use this API.]

#### Use case 1: Query data from a table

Imagine you have a WebAssembly program that needs to query data from a table in a SQL database. The following Rust code shows how you can use the `wasi-sql` interface to execute a SELECT statement and iterate over the resulting rows.

```rs
// Create a prepared statement
let stmt = sql::statement::prepare("SELECT * FROM users WHERE name = ? AND age = ?", vec!["John Doe", "32"])?;

// Execute the query and get the stream of rows
let result_stream = sql::query(stmt)?;

// Iterate over the rows in the stream
for row in result_stream {
    // Print the column names and values for the current row
    println!("Column name: {:?}", row.field_name);
    println!("Value: {:?}", row.value);
}
```

#### Use case 2: Insert data into a table

Imagine you have a WebAssembly program that needs to insert a row into a table in a SQL database. The following Rust code shows how you can use the wasi-sql interface to execute an INSERT statement.

```rs
// Create a prepared statement
let stmt = sql::statement::prepare("INSERT INTO users (name, age) VALUES (?, ?)", vec!["Jane Doe", "30"])?;

// Execute the statement
sql::exec(stmt)?;
```

### Detailed design discussion

[This section should mostly refer to the .wit.md file that specifies the API. This section is for any discussion of the choices made in the API which don't make sense to document in the spec file itself.]

#### [Tricky design choice #1]

[Talk through the tradeoffs in coming to the specific design point you want to make.]

```
// Illustrated with example code.
```

[This may be an open question, in which case you should link to any active discussion threads.]

#### [Tricky design choice 2]

[etc.]

### Considered alternatives

[This section is not required if you already covered considered alternatives in the design discussion above.]

#### [Alternative 1]

[Describe an alternative which was considered, and why you decided against it.]

#### [Alternative 2]

[etc.]

### Stakeholder Interest & Feedback

TODO before entering Phase 3.

[This should include a list of implementers who have expressed interest in implementing the proposal]

### References & acknowledgements

Many thanks for valuable feedback and advice from:

- [Person 1]
- [Person 2]
- [etc.]
