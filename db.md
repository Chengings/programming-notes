# Database

## SQL
📚
 * https://en.wikipedia.org/wiki/SQL_syntax
 * [SQL Language Expressions](https://sqlite.org/lang_expr.html)
 * https://antonz.org/sql-cheatsheet/ #🗄️

### Data Types

Numeric types
- Approximate: `FLOAT`, `REAL`, `DOUBLE`
	- Exact position is in critical
	- Rounding is acceptable
	- For sensor readings, statistical  calculations, graphics
- Exact: `NUMERIC`, `DECIMAL`, `INTEGER`
	- Financial calculations requiring exact precision
	- Any  calculations where rounding errors are unacceptable

 References:
 - https://en.wikipedia.org/wiki/SQL#SQL_data_types
 - [MySQL Reference Manual - Precision Math](https://dev.mysql.com/doc/refman/en/precision-math.html)

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

## MySQL

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

**Check NULL and empty string**

```sql
SELECT * FROM customers WHERE (phone IS NULL OR phone = '');
```

> The meaning of the `NULL` can be regarded as “phone number is not known” and the meaning of the `empty string` can be regarded as “the person is known to have no phone, and thus no phone number.”

[Problems with NULL Values](https://dev.mysql.com/doc/refman/8.0/en/problems-with-null.html)

**Import and export database/table from command line**

Most MySQL commands need to be run with an account, so the "--user user --password" intentionally omitted.

Backup or copy mysql databases via `mysqldump`.
```shell
mysqldump database_name > db.sql
mysqldump database_name table_name > db_table.sql
mysqldump --all-databases > all_dbs.sql
# with routines, triggers and events
mysqldump -u username --password --all-databases --routines --triggers --events > all_dbs.sql
mysqldump --compress database_name > db.sql.gz

# copy data to remote host
mysqldump --opt database_name | mysql --host=remote_host --compress database_name
# backup all databases from remote host
mysqldump --host=remote_host --all-databases > remote_all_dbs.sql

```

> [!warning] If the file is a single-database dump not containing CREATE DATABASE and USE
> The 'your_database' must be created before importing. For example, `mysqladmin create your_database`
```shell
mysql your_database < file.sql
# import gz archive
zcat file.sql.gz | mysql your_database
```

Making a copy of database
```shell
mysqldump db1 > dump.sql
mysqladmin create db2
mysql db2 < dump.sql
```

[mysqldump — A Database Backup Program](https://dev.mysql.com/doc/refman/en/mysqldump.html)
[Using mysqldump for Backups](https://dev.mysql.com/doc/refman/en/using-mysqldump.html)
