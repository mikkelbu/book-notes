https://theartofpostgresql.com/

* Page 9 - SQL Injection - static SQL query text vs. dynamic arguments
* Page 16 - Window functions are executed last in a SQL statement - e.g. after join operations and where clauses.
* Page 19 - Atomic, Consistent, Isolated, Durable
* Page 32 - Correctness and efficiency when using multiple statements
* Page 33 - isolation levels
  * Read uncommitted
  * Read committed
  * Repeatable read
  * Serializable
* Page 37 - lateral join technique
* Page 38 - Don't use procedural code in stored procedures. Use SQL primarily
* Page 39 - The query text of stored procedures are stored on the database server - so less data over the network
* Page 45 - Lateral joins allows one to write "explicit loops" in SQL
* Page 51 - psql - an interactive console - REPL
* Page 53 - `ON_ERROR_ROLLBACK`
* Page 59 - Indentation of SQL (the book suggests to right align top-level SQL clauses) and casing of SQL keywords
* Page 61 - Avoid noise words - `inner` / `outer` - and implicit information in `natural join`
* Page 62 - Use telling relation aliases
* Page 63 - SQL and unit tests
* Page 66 - SQL and regression testing
* Page 67 - `application_name` for additional information in logs and `pg_stat_actipg_stat_activity`
* Page 69 - Index vs. sequential scan. Two kinds of indexes:
  * Backing index for `unique`, `primary key`, `exclude using` (PostgreSQL use index for visibility tricks with its MVCC 
    implementation)
  * Faster data access to data
* Page 70 - MMVC - Multiversion Concurrency Control - makes SQL statements see a snapshot/version of the data as it was at some 
  previous time. MMVC minimizes lock contention.
* Page 72 - Determine which queries to index
* Page 73 - Index types
  * B-Tree - balanced tree -most used index
  * GiST - generalized search tree - 2 dimensional data types - geometry point or ranges data types. Does not support a total 
    order
  * SP-GiST - spaced partitioned gist - non-balanced data structures such as quadtrees, k-d trees, and radix trees (tries)
  * GIN - generalized inverted index - for items that are composite values and used for full text search
  * BRIN - block range indexes - 
  * Hash - can only handle equality comparisons. Do not use has index in PostgreSQL before version 10 (not crash-safe)
  * Bloom filters - used to test whether an element is a member of a set
* See https://www.postgresql.org/docs/14/indexes.html for more index information
* Page 75 - Use the `pg_stat_statements` extension to track planning and execution statistics of all SQL statements executed by a 
  server
* Page 76 - Using `explain` to fix query performance issues
  * Check if there are differences between estimated and actual row counts
  * Sequential scans with a filter step
* Page 87 - SQL - Structured Query Language - is a declarative programming language
* Page 89 - Different areas of SQL
  * DML - data manipulation language - insert, update, and delete statements
  * DDL - data definition language - create, alter, and drop statements
  * TCL - transaction control language - begin/comment/rollback statements ...
  * DCL - data control language - grant and revoke statements
* Page 91 - Select, From, Where
  * Select - only fetch the needed columns. `Select *` also hides problems when relation definitions change
* Page 95 - arguments against `select *` - be specific
* Page 96 - Computed values - `format`, `extract`, `to_char`, `generate_series` ... and aliases
* Page 98 - From clause - https://www.postgresql.org/docs/current/queries-table-expressions.html#QUERIES-FROM
* Page 100 - Where clause - `or` operator is more complex to optimize for. Note that `not in` behaves "odd" when 
  `NULL` values are in the list.
* Page 103 - Order is only guaranteed when using an "order by" clause
* Page 105 - Using order by to implement k nearest neighbours
* Page 109 - Don't use an offset clause to do pagination
* Page 111 - Remember that one can do comparison of composite values - e.g. `and row(lap, position) > (1, 3)`
* Page 114 - Using `lag(nbraces, 1) over(order by decade)` to see the previous value of `nbraces`. PostgreSQL has 
  additional aggregate functions like `bool_and`
* Page 115 - Using `filter(where)` - i.e. `count(*) filter(where position is null) as outs` to only count the rows that 
  pass the filter
* Page 116 - Having clauses are not allowed to reference select output aliases to avoid any ambiguity
* Page 117 - Grouping sets allow one to group by multiple sets of columns - even the empty set - in one pass of the relation
* Page 118 - Syntactic sugar for grouping sets:
  * `rollup` - `rollup(c1, c2, c3)` is syntactic sugar for `(c1, c2, c3), (c1, c2), (c1), ()` (so the assumption is that 
    `c1 > c2 > c3`).
  * `cube` - `cube(c1, c2)` is syntactic sugar for `(c1, c2), (c1), (c2), ()`, so all possible grouping sets based on the
    specified columns.
* Page 120 - Common Table Expressions allow us - using the `with` clause - to run a subquery before and then refer to its result
  like any other relation. It is possible to have multiple CTEs and have later CTEs refer to the previous CTEs.
* Page 124 - `distinct on` can be used to keep only the first row of each set of rows where the given expressions evaluate
  to equal. Note that order is unspecified unless using an `order by` clause.
* Page 125 - Set operations: `union` (`union all`), `intersect`, and `except`.
* Page 129 - `null` is different in SQL - in SQL `null = null` returns `null`. One can use `is distinct from` and
  `is not distinct` for comparisons where "`null` is the same as `null`".
* Page 131 - `not null` constraints
* Page 135 - Window functions - for each row in the input one has access to a "frame" of the data. E.g. `over (order by x)`
  can be read as "order by x rows between unbounded preceding and current row".
* Page 137 - One can use `partition by` to specify "peer rows" - i.e. rows that share a property with the "current row".
* Page 138 - One can use `any` and `all` against a window frame - and similarly for `sum`, `min`, etc.
* Page 139 - It is possible to name a window defition - `window w as (order by position)` - so one can avoid repeating it in
  multiple places. `lag` and `lead` functions to refer to prev and next rows, `ntile(x)` to partition the rows into `x` partitions
* Page 142 - SQL is a strongly typed programming language
* Page 143 - Cross join aka Cartesian product
* Page 144 - Join types: Inner joins, outer joins (left/right), full outer joins, lateral joins
* Page 148 - Use standard SQL for readability - not for portability. 
* Page 154 - Guaranteeing overall consistency - strongly typed data types
* Page 157 - PostgreSQL implements functions and operator polymorphism
* Page 160 - `TABLESAMPLE` to retrieve a subset of the rows in that table
* Page 161 - Boolean data type. Use `is` rather than `=` (due to `null`). Aggregation via `bool_and` and `bool_or`
* Page 163 - Character and Text. Note that "text" and "varchar" are the same, so `varshar(15)` is a text column with the 
  check constraint of 15 characters. There are lots of string functions and operators. There is also support for regular
  expressions - e.g. using regexp_split_to_table` or `regexp_split_to_array`
* Page 167 - full text search with a lot of additional functionality
* Page 168 - server/client encoding
* Page 170 - Numbers. SQL is statically typed, so PostgreSQL must determine the data types of columns for input and output
  before planning and execution.
* Page 172 - Floating point numbers and sequences and serial data type
* Page 174 - Universally Unique Identifier - UUID - 128-bit number
* Page 175 - Bytea and Bitstring and Date/Time and Time Zones - always use timestamps with time zone (it is the same size as
  without).
* Page 178 - We need context for the time - i.e. the timezone.
* Page 179 - Time intervals. PostgreSQL calculates correctly intervals that start as certain dates or timestamps.
* Page 181 - Date/Time Processing and Querying
* Page 183 - `percentile_cont`
* Page 185 - PostgreSQL suppports different network address types: cidr, inet, and macaddr. `set_masklen`
* Page 188 - Ranges - two dimensions of data in a single column, e.g. date-range. One can use
  `exclude using gist (currency with =, validity with &&)` to ensure that we don't have overlapping validity periods for the 
  same currency.
* Page 192 - Denormalized Data Types: Arrays and json. Use array when one is mostly using the array as a whole.

At page 195



# Errata
* Page 93 - "races table has eight column." => races table has eight columns."
* Page 108 - `decades.decade` is not needed in `group by decades.decade, drivers.driverid` as we already use this in the filter
* Page 139 - I guess `over(order by fastestlapspeed::numeric)` should be ordered descending to match "his position in terms
  offastest lap speed". Also the text on page 140 is wrong as "Gutiérrez" and "Sutil" had the slowest fastestlapspeed
* Page 190 - `\index{Operators!@}` looks like a LaTeX error (I guess due to the special characters)
* Page 378 - `\index{Operators!%}` looks like a LaTeX error. The same kind of error on 379.