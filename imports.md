<h1><a name="imports">World imports</a></h1>
<ul>
<li>Imports:
<ul>
<li>interface <a href="#wasi:sql_types_0.2.0_draft"><code>wasi:sql/types@0.2.0-draft</code></a></li>
<li>interface <a href="#wasi:sql_readwrite_0.2.0_draft"><code>wasi:sql/readwrite@0.2.0-draft</code></a></li>
</ul>
</li>
</ul>
<h2><a name="wasi:sql_types_0.2.0_draft"></a>Import interface wasi:sql/types@0.2.0-draft</h2>
<hr />
<h3>Types</h3>
<h4><a name="data_type"></a><code>variant data-type</code></h4>
<p>common data types</p>
<h5>Variant Cases</h5>
<ul>
<li><a name="data_type.int32"></a><code>int32</code>: <code>s32</code></li>
<li><a name="data_type.int64"></a><code>int64</code>: <code>s64</code></li>
<li><a name="data_type.uint32"></a><code>uint32</code>: <code>u32</code></li>
<li><a name="data_type.uint64"></a><code>uint64</code>: <code>u64</code></li>
<li><a name="data_type.float"></a><code>float</code>: <code>float64</code></li>
<li><a name="data_type.double"></a><code>double</code>: <code>float64</code></li>
<li><a name="data_type.str"></a><code>str</code>: <code>string</code></li>
<li><a name="data_type.boolean"></a><code>boolean</code>: <code>bool</code></li>
<li><a name="data_type.date"></a><code>date</code>: <code>string</code></li>
<li><a name="data_type.time"></a><code>time</code>: <code>string</code></li>
<li><a name="data_type.timestamp"></a><code>timestamp</code>: <code>string</code></li>
<li><a name="data_type.binary"></a><code>binary</code>: list&lt;<code>u8</code>&gt;</li>
<li><a name="data_type.null"></a><code>null</code></li>
</ul>
<h4><a name="row"></a><code>record row</code></h4>
<p>one single row item</p>
<h5>Record Fields</h5>
<ul>
<li><a name="row.field_name"></a><code>field-name</code>: <code>string</code></li>
<li><a name="row.value"></a><code>value</code>: <a href="#data_type"><a href="#data_type"><code>data-type</code></a></a></li>
</ul>
<h4><a name="statement"></a><code>resource statement</code></h4>
<p>allows parameterized queries
e.g., prepare(&quot;SELECT * FROM users WHERE name = ? AND age = ?&quot;, vec![&quot;John Doe&quot;, &quot;32&quot;])</p>
<h4><a name="error"></a><code>resource error</code></h4>
<p>An error resource type.
Currently, this provides only one function to return a string representation
of the error. In the future, this will be extended to provide more information.</p>
<h4><a name="connection"></a><code>resource connection</code></h4>
<h2>A connection to a sql store.</h2>
<h3>Functions</h3>
<h4><a name="static_statement.prepare"></a><code>[static]statement.prepare: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="static_statement.prepare.query"></a><a href="#query"><code>query</code></a>: <code>string</code></li>
<li><a name="static_statement.prepare.params"></a><code>params</code>: list&lt;<code>string</code>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_statement.prepare.0"></a> result&lt;own&lt;<a href="#statement"><a href="#statement"><code>statement</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="method_error.trace"></a><code>[method]error.trace: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="method_error.trace.self"></a><code>self</code>: borrow&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="method_error.trace.0"></a> <code>string</code></li>
</ul>
<h4><a name="static_connection.open"></a><code>[static]connection.open: func</code></h4>
<h5>Params</h5>
<ul>
<li><a name="static_connection.open.name"></a><code>name</code>: <code>string</code></li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="static_connection.open.0"></a> result&lt;own&lt;<a href="#connection"><a href="#connection"><code>connection</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h2><a name="wasi:sql_readwrite_0.2.0_draft"></a>Import interface wasi:sql/readwrite@0.2.0-draft</h2>
<hr />
<h3>Types</h3>
<h4><a name="statement"></a><code>type statement</code></h4>
<p><a href="#statement"><a href="#statement"><code>statement</code></a></a></p>
<p>
#### <a name="row"></a>`type row`
[`row`](#row)
<p>
#### <a name="error"></a>`type error`
[`error`](#error)
<p>
#### <a name="connection"></a>`type connection`
[`connection`](#connection)
<p>
----
<h3>Functions</h3>
<h4><a name="query"></a><code>query: func</code></h4>
<p>query is optimized for querying data, and
implementors can make use of that fact to optimize
the performance of query execution (e.g., using
indexes).</p>
<h5>Params</h5>
<ul>
<li><a name="query.c"></a><code>c</code>: borrow&lt;<a href="#connection"><a href="#connection"><code>connection</code></a></a>&gt;</li>
<li><a name="query.q"></a><code>q</code>: borrow&lt;<a href="#statement"><a href="#statement"><code>statement</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="query.0"></a> result&lt;list&lt;<a href="#row"><a href="#row"><code>row</code></a></a>&gt;, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
<h4><a name="exec"></a><code>exec: func</code></h4>
<p>exec is for modifying data in the database.</p>
<h5>Params</h5>
<ul>
<li><a name="exec.c"></a><code>c</code>: borrow&lt;<a href="#connection"><a href="#connection"><code>connection</code></a></a>&gt;</li>
<li><a name="exec.q"></a><code>q</code>: borrow&lt;<a href="#statement"><a href="#statement"><code>statement</code></a></a>&gt;</li>
</ul>
<h5>Return values</h5>
<ul>
<li><a name="exec.0"></a> result&lt;<code>u32</code>, own&lt;<a href="#error"><a href="#error"><code>error</code></a></a>&gt;&gt;</li>
</ul>
