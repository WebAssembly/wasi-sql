# `wasi-sql` API

## Interfaces

```wit
interface "wasi:sql" {
    // one single row item
    record row {
        field-name: string,
        value: data-type,
    }
    
    // common data types
    variant data-type {
        int32(s32),
        int64(s64),
        uint32(u32),
        uint64(u64),
        float(float64),
        double(float64),
        str(string),
        boolean(bool),
        date(string),
        time(string),
        timestamp(string),
        binary(list<u8>),
        null
    }
    
    // allows parameterized queries
    resource statement {
        // e.g., create("SELECT * FROM users WHERE name = ? AND age = ?", vec!["John Doe", "32"])
        prepare: func(query: string, params: list<string>) -> result<statement, sql-error>
    }
    
    // query is optimized for querying data, and 
    // implementors can make use of that fact to optimize 
    // the performance of query execution (e.g., using
    // indexes).
    query: func(q: statement) -> result<stream<row>, sql-error>
    
    // exec is for modifying data in the database.
    exec: func(q: statement) -> result<_, sql-error>
    
    // common error types
    variant sql-error {
        syntax-error(string),
        constraint-violation(string),
        access-violation(string),
        unexpected-error(string)
    }
}
```

## Worlds

```wit
world "wasi:sql/http-sql" {
    import sql: "wasi:sql"
    
    export handle-create: "wasi:http/handler"
    export handle-read: "wasi:http/handler"
    export handle-update: "wasi:http/handler"
    export handle-delete: "wasi:http/handler"
}
```