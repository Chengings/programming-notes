# Database

## SQL
📚
 * https://en.wikipedia.org/wiki/SQL_syntax
 * [SQL Language Expressions](https://sqlite.org/lang_expr.html)

### Views

```sql
CREATE VIEW myview AS
    SELECT name, temp_lo, temp_hi, prcp, date, location
        FROM weather, cities
        WHERE city = name;

SELECT * FROM myview;
```

Views are a special version of tables in SQL. They provide a virtual table environment for various complex operations. You can select data from multiple tables, or you can select specific data based on certain criteria in views https://www.datacamp.com/community/tutorials/views-in-sql

Views are read-only in SQLite

References:
* https://en.wikipedia.org/wiki/View_(SQL)
* https://dev.mysql.com/doc/refman/8.0/en/views.html
* https://www.postgresql.org/docs/current/tutorial-views.html
* https://www.sqlite.org/lang_createview.html

## SQLite

SQLite doesn't suitable for these use cases
* Remote data
* Big data
* Concurrent writers
* Gazillion transactions/second

Source: [sqlite.org talks](https://www.sqlite.org/talks/cmu-20150917.odp)

📦
 * "SQL.js" allows you to create a relational database and query it entirely in the browser https://github.com/sql-js/sql.js
 * "Litestream" is a standalone streaming replication tool for SQLite. It runs as a background process and safely replicates changes incrementally to another file or S3. https://github.com/benbjohnson/litestream

Gist
 * Avoid putting SQLite database files **on NFS** if multiple processes might try to access the file at the same time. https://www.sqlite.org/faq.html#q5

# MySQL

📚
- [MySQL 8.0 Reference Manual](https://dev.mysql.com/doc/refman/8.0/en/)
	- [SELECT statement](https://dev.mysql.com/doc/refman/8.0/en/select.html)
	- [UPDATE statement](https://dev.mysql.com/doc/refman/8.0/en/update.html)
	- [JOIN clause](https://dev.mysql.com/doc/refman/8.0/en/join.html)
	- Functions and operators
		- [Built-in such as `=`, `<>`, `DATE()`, `LIKE()`, `FLOOR()`](https://dev.mysql.com/doc/refman/8.0/en/built-in-function-reference.html)
		- [String (including regular expression)](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html)

**Duplicate Table**

Use `CREATE TABLE ... LIKE` and `INSERT ... SELECT`.
```sql
-- create an EMPTY table BASED on the DEFINITION of another table, including any column ATTRIBUTES and INDEXES defined
CREATE TABLE new_tbl LIKE orig_tbl

INSERT INTO new_tbl SELECT * FROM orig_tbl
```

There is a one liner `CREATE TABLE ... SELECT` statement. Unlike above, this "create table select" statement doesn't preserve/create attributes and indexes.

[CREATE TABLE ... LIKE](https://dev.mysql.com/doc/refman/8.0/en/create-table-like.html) and [CREATE TABLE ... SELECT](https://dev.mysql.com/doc/refman/8.0/en/create-table-select.html)