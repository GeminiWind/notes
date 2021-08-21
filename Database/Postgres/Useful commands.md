# Useful commands

## Upsert (insert or update)

To use the upsert feature in PostgreSQL, you use the `INSERT ON CONFLICT` statement as follows:

`INSERT INTO table_name(column_list) 
VALUES(value_list)
ON CONFLICT target action;`

Code language: SQL (Structured Query Language) (sql)

PostgreSQL added the `ON CONFLICT target action` clause to the `INSERT` statement to support the upsert feature.

In this statement, the `target` can be one of the following:

-    `(column_name)` – a column name.
-    `ON CONSTRAINT constraint_name` – where the constraint name could be the name of the [UNIQUE constraint](https://www.postgresqltutorial.com/postgresql-unique-constraint/).
-    `WHERE predicate` – a [WHERE clause](https://www.postgresqltutorial.com/postgresql-where/) with a predicate.

The `action` can be one of the following:

-    `DO NOTHING` – means do nothing if the row already exists in the table.
-    `DO UPDATE SET column_1 = value_1, .. WHERE condition` – update some fields in the table.

Notice that the `ON CONFLICT` clause is only available from PostgreSQL 9.5. If you are using an earlier version, you will need a workaround to have the upsert feature.