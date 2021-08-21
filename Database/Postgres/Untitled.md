https://use-the-index-luke.com/sql/where-clause/functions/case-insensitive-search

## search ignore case sentive

- Use one function to index like

```sql
CREATE INDEX template_name_idx ON template(UPPER (name))
```

## order of search
- Equality first, then range after (>=, <=, BETWEEN .. AND)

## using LIKE

- Only the part before the first wild card serves as an access predicate.

The remaining characters do not narrow the scanned index range—non-matching entries are just left out of the result
 - Avoid `LIKE` expressions with leading wildcards (e.g., `'%TERM'`).

## partial index

