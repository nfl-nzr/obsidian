#### pg_dump
This is used for selective back up.
Backs up to plain SQL but can also do tar files 
Eg: Creates a compressed, single database backup: pg_dump -h localhost -p 5432 -U someuser -F c -b -v -f mydb.backup mydb
### pg_dumpall
Used for backing up all the databases. Will be slower.

### Terminate active connections
Active connections need to be terminated before database can be backed up and restored.
The following command lists the active connections

pg_stat_activity (SELECT * FROM pg_stat_activity;) is a view that will list currently active connections and the process id. It will also list the active query that is running

To terminate all connections and kill active queries use

pg_terminate_backend(procid) (SELECT pg_terminate_backend(procid);) will kill a specific connection. All running queries will automatically cancel. This will be your weapon of choice prior to a restore to prevent an eager user from immediately restarting a cancelled query.


timestamp::The actual storage of a `timestamptz` does not store any time zone data. It stores all values in UTC. The time zone aspect comes into play when inputting and outputting the timestamp data. When you input a `timestamptz`, PostgreSQL will assume the timestamp is in the time zone set by the `TimeZone` configuration parameter, and it will convert it to UTC for storage. When you retrieve a `timestamptz`, PostgreSQL will convert the UTC value to the time zone specified by the `TimeZone` parameter before displaying it.

 ### Common database objects in postgres

**server** ::The PostgreSQL server service is often just called a PostgreSQL server, or daemon. You can have more than one a physical server as long as they listen on different ports or IPs and have different places to store their respective data.

databases::Each PostgreSQL server houses many databases.

table::Table are the workhorses of any database. What is unique about PostgreSQL tables is the inheritance support and the fact that every table automatically begets an accompanying custom data type. Tables can inherit from other tables and querying can bring up child records from child tables.

schema::Schemas are part of the ANSI-SQL standards, so you’ll see them in other databases. Schemas are the logical containers of tables and other objects. Each database can have multiple schemas.

tablespace::Tablespace is the physical location where data is stored. PostgreSQL allows tablespaces to be independently managed, which means you can easily move databases to different drives with just a few commands. 

view::Most relational databases have views for abstracting queries. In PostgreSQL, you can also have views that can be updated.

function:: Functions in PostgreSQL can return scalar value or sets of records. Aggregates are functions used with SQL constructs such as GROUP BY to summarize data. Most of the time, they return scalars but in PostgreSQL they can return composite objects.

operator::These are symbolic functions that have backing of a function. In PostgreSQL, you can define your own.

cast::Casts allow you to convert from one data type to another. They are supported by functions that actually perform the conversion. What is rare about PostgreSQL that you won’t find with many other databases is that you can create your own casts and thus change the default behavior of casting. Casting can be implicit or explicit. Implicit casts are automatic and usually will expand from a more specific to a more generic type. When an implicit cast is not offered, you must cast explicitly.

sequence::Sequence is what controls auto-incrementation in table definitions. They are usually automatically created when you define a serial column. Because they are objects in their own right, you could have multiple serial columns use the same sequence object, effectively achieveing uniqueness not only within the column but across them.

trigger::Found in many databases, triggers detect data change events and can react before or after the actual data is changed. PostgreSQL 9.0 introduced some special twists to this with the WHEN clause. PostgreSQL 9.1 added the extra feature of making triggers available for views.

foreign data wrappers::Foreign data wrappers allow you to query a remote data source whether that data source be another relational database server, flat file, a NoSQL database, a web service or even an application platform like SalesForce.

row/record::Rows and records generally mean the same thing. In PostgreSQL, rows can be treated independently from their respective tables. This distinction becomes apparent and useful when you write functions or use the row constructor in SQL.

extension::This is a new feature introduced in 9.1 that packages a set of functions, types, casts, indexes, and so forth into a single unit for maintainability. It is similar in concept to Oracle packages and is primarily used to deploy add-ons.

postgresql.conf::controls general settings, such as how much memory to allocate, default storage location for new databases, which IPs PostgreSQL listens on, where logs are stored, and so forth.


pg_hba.conf::controls security. It manages access to the server, dictating which users can login into which databases, which IPs or groups of IPs are permitted to connect and the authentication scheme expected.
### Interactive
This is when you run the psql command. Help can be opened by running \d?
For help with a query run \h <query>

### Non interactive
Non-interactive commands means that you ask psql to execute a script file composed of a mix of SQL statements and psql commands. You can alternatively pass one or more SQL statements. 

### Timing
Used to output the time it took for a query to run. Can be turned on using the \timing option.

### Auto commit
 By default postgres commits the query as soon as it is run. Auto commit can be turned off with the \set AUTOCOMMIT <off||on>. Once turned off queries need to be manually committed with COMMIT; or rolled back with ROLLBACK;

### Shortcuts
The \set command is also useful for defining user-defined shortcuts. You may want to store the shortcuts in your psqlrc file to have them available each time. For example, if you use EXPLAIN ANALYZE VERBOSE all the time and you’re tired of typing it all out, you can define a variable as follows: \set eav 'EXPLAIN ANALYZE VERBOSE' Now whenever you want to do an EXPLAIN ANALYZE VERBOSE of a query, you prefix it with :eav (colon resolves the variable): :eav SELECT COUNT(*) FROM pg_tables; You can even save commonly used queries as strings in your psqlrc startup script as we did for qstats91 and qstats92. So, if I am on a PostgreSQL 9.2 database, I can see current activity by just typing the following: :qstats92

## Triggers
