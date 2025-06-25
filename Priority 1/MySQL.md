# MySQL

## Database Operations
- `CREATE DATABASE dbname;` - Create new database
- `USE dbname;` - Select database to work with
- `DROP DATABASE dbname;` - Delete database
- `SHOW DATABASES;` - List all databases

## Table Operations
### Create/Modify Tables
- `CREATE TABLE tablename (col1 datatype, col2 datatype);` - Basic table creation
- `CREATE TABLE tablename (id INT AUTO_INCREMENT PRIMARY KEY, name VARCHAR(50));` - With primary key
- `ALTER TABLE tablename ADD COLUMN newcol datatype;` - Add column
- `ALTER TABLE tablename DROP COLUMN colname;` - Remove column
- `ALTER TABLE tablename MODIFY COLUMN colname newdatatype;` - Change column type
- `DROP TABLE tablename;` - Delete table
- `TRUNCATE TABLE tablename;` - Delete all data but keep table
- `RENAME TABLE oldname TO newname;` - Change table name

## Data Querying
### Basic SELECT
- `SELECT * FROM tablename;` - Get all data
- `SELECT col1, col2 FROM tablename;` - Specific columns
- `SELECT DISTINCT col1 FROM tablename;` - Unique values
- `SELECT COUNT(*) FROM tablename;` - Count rows

### Filtering
- `SELECT * FROM tablename WHERE condition;` - Basic filter
- `SELECT * FROM tablename WHERE col1 = 'value';` - Exact match
- `SELECT * FROM tablename WHERE col1 LIKE 'A%';` - Starts with A
- `SELECT * FROM tablename WHERE col1 IN (1,2,3);` - Multiple values
- `SELECT * FROM tablename WHERE col1 BETWEEN 10 AND 20;` - Range
- `SELECT * FROM tablename WHERE col1 IS NULL;` - Null values

### Sorting/Limiting
- `SELECT * FROM tablename ORDER BY col1;` - Sort ascending
- `SELECT * FROM tablename ORDER BY col1 DESC;` - Sort descending
- `SELECT * FROM tablename LIMIT 10;` - First 10 rows
- `SELECT * FROM tablename LIMIT 5,10;` - Rows 6-15

## Data Modification
### Insert
- `INSERT INTO tablename VALUES (val1, val2);` - Insert all columns
- `INSERT INTO tablename (col1,col2) VALUES (val1,val2);` - Specific columns
- `INSERT INTO tablename SELECT * FROM othertable;` - Copy data

### Update
- `UPDATE tablename SET col1 = value WHERE condition;` - Basic update
- `UPDATE tablename SET col1 = col1 + 1 WHERE id = 5;` - Increment value

### Delete
- `DELETE FROM tablename WHERE condition;` - Delete specific rows
- `DELETE FROM tablename;` - Delete all rows (be careful!)

## Joins
- `SELECT * FROM table1 INNER JOIN table2 ON table1.id = table2.id;` - Inner join
- `SELECT * FROM table1 LEFT JOIN table2 ON table1.id = table2.id;` - Left join
- `SELECT * FROM table1 RIGHT JOIN table2 ON table1.id = table2.id;` - Right join
- `SELECT * FROM table1 CROSS JOIN table2;` - Cross join (cartesian product)

## Aggregation
- `SELECT COUNT(*) FROM tablename;` - Count rows
- `SELECT SUM(col1) FROM tablename;` - Sum values
- `SELECT AVG(col1) FROM tablename;` - Average
- `SELECT MIN(col1), MAX(col1) FROM tablename;` - Min/max
- `SELECT col1, COUNT(*) FROM tablename GROUP BY col1;` - Group with count
- `SELECT col1, SUM(col2) FROM tablename GROUP BY col1 HAVING SUM(col2) > 100;` - Group with filter

## Advanced Features
### Indexes
- `CREATE INDEX idx_name ON tablename(colname);` - Create index
- `SHOW INDEX FROM tablename;` - View indexes
- `DROP INDEX idx_name ON tablename;` - Remove index

### Views
- `CREATE VIEW viewname AS SELECT col1,col2 FROM tablename;` - Create view
- `SELECT * FROM viewname;` - Use view
- `DROP VIEW viewname;` - Delete view

### Stored Procedures
```sql
DELIMITER //
CREATE PROCEDURE proc_name(IN param INT)
BEGIN
  SELECT * FROM tablename WHERE id = param;
END //
DELIMITER ;
```

- CALL proc_name(5); - Execute procedure
- DROP PROCEDURE proc_name; - Remove procedure

### Transactions
- START TRANSACTION; - Begin transaction
- COMMIT; - Save changes
- ROLLBACK; - Undo changes

### Utility Commands
- SHOW TABLES; - List tables in database
- DESCRIBE tablename; - Show table structure
- EXPLAIN SELECT...; - Show query execution plan
- SHOW PROCESSLIST; - View active connections































