https://www.packtpub.com/product/mastering-postgresql-15-fifth-edition/9781803248349

Code at https://github.com/PacktPublishing/Mastering-PostgreSQL-15

# PostgreSQL 15 Overview
* Page 2 - predefined user roles in PostgreSQL
* Page 9 - `id int UNIQUE NULLS NOT DISTINCT` for treating `NULL`s as equal in the index
* Page 10 - The `merge` command - more flexible than just an "upsert"
* Page 14 - `pg_basebackup` supports backups compressed on the server side

# Understanding Transactions and Locking
* Page 19 - `BEGIN`, `COMMIT`, and `ROLLBACK`
* Page 20 - `COMMIT AND CHAIN;` vs `COMMIT AND NO CHAIN;`
* Page 22 - `SAVEPOINT [name]`
* Page 23 - In PostgreSQL almost all DDL are transactional 
* Page 25 - MVCC - Multi-Version Concurrency Control. A transaction can only see the updates that
  have been committed before the initiation of the transition. Note that write transactions does not
  block read transactions, but write transactions can block other writes.
* Page 27 - Explicit locking - 8 different lockmodes 
* Page 28 - `pg_stat_activity` to see the current activity of the server processes
* Page 29 - Scalable autoincrement (with no holes) using CTE
* Page 30 - `FOR UPDATE` / `FOR UPDATE NOWAIT` / `FOR UPDATE SKIP LOCKED`
* Page 32 - `FOR UPDATE` can also lock tables referenced by FK
* Page 33 - `FOR NO KEY UPDATE`, `FOR SHARE`, and `FOR KEY SHARE`
* Page 34 - `REPEATABLE READ` -  use the same snapshot throughout the entire transaction
* Page 35 - 3 isolation levels. `Read Uncommitted` is the same as `Read committed` - only use `serializable`
  when you understand the effects
* Page 37 - `deadlock_timeout` to resolve deadlocks. `ctid` the unique identificer of a row in a table
  (physical position). `ORDER BY ctid DESC` reads the table backwards in physical order
* Page 38 - `ERROR: could not serialize access due to concurrent update` - can be fixed by retry logic in application
* Page 39 - advisory locks - locking a number (and not affected by transactions)
* Page 40 - async cleanup due to MVCC - `VACUUM`. This will not affect the table size (in most cases)
* Page 42 - `VACUUM` to update the visibility map (for index-only scans) and for setting the watermark for
  transaction ID wraparound
* Page 43 - `pg_squeeze` extension instead of `VACUUM FULL` to rewrite a table without blocking writes
* Page 44 - `SELECT pg_size_pretty(pg_relation_size('table_name'));` and example showing how the `UPDATE`
  operation copies rows.
* Page 45 - Understanding storage is the key to performance and administration in general.
* Page 46 - If `VACUUM`` only finds dead rows after a certain position in the table, it can return
  space to the filesystem
* Page 47 - Old transactions can keep old rows alive - can be tweaked by `old_snapshot_threshold`

# Making Use of Indexes
* Page 49 - One cannot have good performance without proper indexing


# Errata
* Page 2 - "With the introduction of PostgreSQL," => "With the introduction of PostgreSQL 15,"
* Page 8 - "Since PostgreSQL, it" => Since PostgreSQL 15, it"
* Page 14 - Link `https://www.postgresql.org/docs/15/sql-altersubscription` is missing `.html`
* Page 23 - "previously defined savepoin" => "previously defined savepoint"
* Page 23 - Link `https://www.postgresql.org/docs/15/sql-release-savepoint` is missing `.html`
* Page 24 - "BEGI" => "BEGIN"
* Page 48 - There are no answers at https://github.com/PacktPublishing/Mastering-PostgreSQL-15-, some
  can be found at https://github.com/PacktPublishing/Mastering-PostgreSQL-13-Fourth-Edition/blob/master/Assessment.pdf
