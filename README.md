# Indexing in SQL

## What is Indexing?
Indexing in SQL is a technique used to speed up the retrieval of data from a database table. An index is a data structure that improves the efficiency of SELECT queries by reducing the number of rows that need to be scanned.

## Types of Indexes

1. **Primary Index** - Automatically created when a primary key is defined.
2. **Unique Index** - Ensures that all values in the indexed column are unique.
3. **Clustered Index** - Determines the physical order of data in a table (one per table).
4. **Non-Clustered Index** - A separate structure that maintains pointers to the actual data.
5. **Composite Index** - Index on multiple columns.
6. **Full-Text Index** - Used for searching text-based data efficiently.

## Creating an Index
```sql
-- Creating a simple index
CREATE INDEX idx_customer_name
ON customers(name);
```

## Creating a Unique Index
```sql
CREATE UNIQUE INDEX idx_unique_email
ON users(email);
```

## Creating a Composite Index
```sql
CREATE INDEX idx_order_details
ON orders(customer_id, order_date);
```

## Clustered vs Non-Clustered Index
```sql
-- Creating a Clustered Index
CREATE CLUSTERED INDEX idx_customer_id
ON customers(customer_id);

-- Creating a Non-Clustered Index
CREATE NONCLUSTERED INDEX idx_customer_city
ON customers(city);
```

## Dropping an Index
```sql
DROP INDEX idx_customer_name;
```

## When to Use Indexes
- Use indexes on columns that are frequently used in WHERE clauses.
- Use indexes on JOIN conditions to speed up query performance.
- Avoid indexing columns with low selectivity (e.g., columns with many duplicate values).
- Do not overuse indexes, as they can slow down INSERT, UPDATE, and DELETE operations.

## Checking Index Usage
```sql
-- PostgreSQL: Check index usage
SELECT * FROM pg_indexes WHERE tablename = 'customers';
```

## Example Query Performance Improvement
Without Index:
```sql
SELECT * FROM orders WHERE order_date = '2024-01-01';
```
With Index:
```sql
CREATE INDEX idx_order_date ON orders(order_date);
SELECT * FROM orders WHERE order_date = '2024-01-01';
```

Adding an index reduces the time taken for queries, improving database efficiency.
