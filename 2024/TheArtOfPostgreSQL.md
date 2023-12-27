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
* Page 116 - Having clauses are not allowed to reference select output aliases to avoid any ambiguity


# Errata
* Page 93 - "races table has eight column." => races table has eight columns."
* Page 108 - `decades.decade` is not needed in `group by decades.decade, drivers.driverid` as we already use this in the filter