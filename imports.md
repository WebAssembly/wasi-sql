<h1><a name="imports">World imports</a></h1>
<ul>
<li>Imports:
<ul>
<li>interface <a href="#wasi:sql_types_0.1.0"><code>wasi:sql/types@0.1.0</code></a></li>
<li>interface <a href="#wasi:sql_readwrite_0.1.0"><code>wasi:sql/readwrite@0.1.0</code></a></li>
</ul>
</li>
</ul>
<h2><a name="wasi:sql_types_0.1.0">Import interface wasi:sql/types@0.1.0</a></h2>
<hr />
<h3>Types</h3>
<h4><a name="data_type"><code>variant data-type</code></a></h4>
<p>common data types</p>
<h5>Variant Cases</h5>
<ul>
<li><a name="data_type.int32"><code>int32</code></a>: <code>s32</code></li>
<li><a name="data_type.int64"><code>int64</code></a>: <code>s64</code></li>
<li><a name="data_type.uint32"><code>uint32</code></a>: <code>u32</code></li>
<li><a name="data_type.uint64"><code>uint64</code></a>: <code>u64</code></li>
<li><a name="data_type.float"><code>float</code></a>: <code>float64</code></li>
<li><a name="data_type.double"><code>double</code></a>: <code>float64</code></li>
<li><a name="data_type.str"><code>str</code></a>: <code>string</code></li>
<li><a name="data_type.boolean"><code>boolean</code></a>: <code>bool</code></li>
<li><a name="data_type.date"><code>date</code></a>: <code>string</code></li>
<li><a name="data_type.time"><code>time</code></a>: <code>string</code></li>
<li><a name="data_type.timestamp"><code>timestamp</code></a>: <code>string</code></li>
<li><a name="data_type.binary"><code>binary</code></a>: list&lt;<code>u8</code>&gt;</li>
<li><a name="data_type.null"><code>null</code></a></li>
</ul>
<h4><a name="row"><code>record row</code></a></h4>
<p>one single row item</p>
<h5>Record Fields</h5>
<ul>
<li><a name="row.field_name"><code>field-name</code></a>: <code>string</code></li>
<li><a name="row.value"><code>value</code></a>: <a href="#data_type"><a href="#data_type"><code>data-type</code></a></a></li>
</ul>
<h4><a name="statement"><code>resource statement</code></a></h4>
<p>allows parameterized queries
e.g., prepare(&quot;SELECT * FROM users WHERE name = ? AND age = ?&quot;, vec![&quot;John Doe&quot;, &quot;32&quot;])</p>
<h4><a name="error"><code>resource error</code></a></h4>
<p>An error resource type.
Currently, this provides only one function to return a string representation
of the error. In the future, this will be extended to provide more information.</p>
<h4><a name="connection"><code>resource connection</code></a></h4>
<h2>A connection to a sql store.</h2>
<h3>Functions</h3>
<h4><a name="static_statement.prepare"><code>[static]statement.prepare: func</code></a></h4>
<h5>Params</h5>
<ul>
<li><a name="static_statement.prepare.query"><a href="#query"><code>query</code></a></a>: <code>string</code></li>
<li><a name="static_statement.prepare.params"><code>params</code></a>: list&lt;<code>string</code>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_statement.prepare.0"></a> result&lt;own&lt;<a href="#statement"><a href="#statement"><code>statement</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="method_error.trace"><code>[method]error.trace: func</code></a></h4>
<h5>Params</h5>
<ul>
<li><a name="method_error.trace.self"><code>self</code></a>: borrow&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_error.trace.0"></a> <code>string</code></li>
</ul>
<h4><a name="static_connection.open"><code>[static]connection.open: func</code></a></h4>
<h5>Params</h5>
<ul>
<li><a name="static_connection.open.name"><code>name</code></a>: <code>string</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_connection.open.0"></a> result&lt;own&lt;<a href="#connection"><a href="#connection"><code>connection</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h2><a name="wasi:sql_readwrite_0.1.0">Import interface wasi:sql/readwrite@0.1.0</a></h2>
<hr />
<h3>Types</h3>
<h4><a name="statement"><code>type statement</code></a></h4>
<p><a href="#statement"><a href="#statement"><code>statement</code></a></a></p>
<p>
#### <a name="row">`type row`</a>
[`row`](#row)
<p>
#### <a name="error">`type error`</a>
[`error`](#error)
<p>
#### <a name="connection">`type connection`</a>
[`connection`](#connection)
<p>
----
<h3>Functions</h3>
<h4><a name="query"><code>query: func</code></a></h4>
<p>query is optimized for querying data, and
implementors can make use of that fact to optimize
the performance of query execution (e.g., using
indexes).</p>
<h5>Params</h5>
<ul>
<li><a name="query.c"><code>c</code></a>: borrow&lt;<a href="#connection"><a href="#connection"><code>connection</code></a></a>&gt;</li>
<li><a name="query.q"><code>q</code></a>: borrow&lt;<a href="#statement"><a href="#statement"><code>statement</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="query.0"></a> result&lt;list&lt;<a href="#row"><a href="#row"><code>row</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="exec"><code>exec: func</code></a></h4>
<p>exec is for modifying data in the database.</p>
<h5>Params</h5>
<ul>
<li><a name="exec.c"><code>c</code></a>: borrow&lt;<a href="#connection"><a href="#connection"><code>connection</code></a></a>&gt;</li>
<li><a name="exec.q"><code>q</code></a>: borrow&lt;<a href="#statement"><a href="#statement"><code>statement</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="exec.0"></a> result&lt;<code>u32</code>, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
