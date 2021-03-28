# Database

---

## SQL
📚
 * https://en.wikipedia.org/wiki/SQL_syntax
 * [SQL Language Expressions](https://sqlite.org/lang_expr.html)

## SQLite
📦
 * "SQL.js" allows you to create a relational database and query it entirely in the browser https://github.com/sql-js/sql.js
 * "Litestream" is a standalone streaming replication tool for SQLite. It runs as a background process and safely replicates changes incrementally to another file or S3. https://github.com/benbjohnson/litestream

Gist
 * Avoid putting SQLite database files **on NFS** if multiple processes might try to access the file at the same time. https://www.sqlite.org/faq.html#q5
