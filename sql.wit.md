# `wasi-sql` API

## Interfaces

```wit
interface "wasi:sql" {
    // iterator item type
    resource row {
        field-name: list<string>
        values: list<data-types>
        index: u32
    }
    
    // common data types
    variant data-types {
        integer(s32),
        float(float64),
        str(string),
        boolean(bool),
        date(string),
        time(string),
        timestamp(string),
        binary(list<u8>),
    }
    
    // iterator for rows
    resource sql-result {
        next: func() -> option<row>
    }
    
    // allows parameterized queries
    resource statement {
        // e.g., create("SELECT * FROM users WHERE name = ? AND age = ?", vec!["John Doe", "32"])
        create: func(s: string, p: list<string>) -> result<statement, error>
    }
    
    // query is optimized for querying data, and 
    // implementors can make use of that fact to optimize 
    // the performance of query execution (e.g., using
    // indexes).
    query: func(q: statement) -> result<sql-result, error>
    
    // exec is for modifying data in the database.
    exec: func(q: statement) -> result<_, error>
    
    // common error types
    enum error {
        syntax-error(string),
        constraint-violation(string),
        access-violation(string)
    }
}
```

## Worlds

```
world "wasi:sql/http-sql" {
    import sql: "wasi:sql"
    
    export handle-create: "wasi:http/handler"
    export handle-read: "wasi:http/handler"
    export handle-update: "wasi:http/handler"
    export handle-delete: "wasi:http/handler"
}
```