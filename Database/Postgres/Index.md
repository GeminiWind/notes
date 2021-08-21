# Indexes

## B-Tree

B-trees can handle equality and range queries on data that can be sorted into some ordering. In particular, the PostgreSQL query planner will consider using a B-tree index whenever an indexed column is involved in a comparison using one of these operators:

<

<=

=

>=

>

Constructs equivalent to combinations of these operators, such as BETWEEN and IN, can also be implemented with a B-tree index search. Also, an IS NULL or IS NOT NULL condition on an index column can be used with a B-tree index.

The optimizer can also use a B-tree index for queries involving the pattern matching operators LIKE and ~ if the pattern is a constant and is anchored to the beginning of the string — for example, col LIKE 'foo%' or col ~ '^foo', but not col LIKE '%bar'.

## Hash indexes

Hash indexes can handle only simple equality comparison (=). It means that whenever an indexed column is involved in a comparison using the equal(=) operator, the query planner will consider using a hash index.

To create a hash index, you use the `CREATE INDEX` statement with the `HASH` index type in the `USING` clause as follows:

`CREATE INDEX index_name 
ON table_name USING HASH (indexed_column);`

## GIN indexes

GIN stands for **g**eneralized **in**verted indexes. It is commonly referred to as GIN.

GIN indexes are most useful when you have multiple values stored in a single column, for example, [hstore](https://www.postgresqltutorial.com/postgresql-hstore/), [array](https://www.postgresqltutorial.com/postgresql-array/), jsonb, and range types.