
Select
```sql
-- Single field
SELECT id FROM users;

-- Multiple fields
SELECT id, name FROM users;

-- All Fields
SELECT * FROM users;
```

Create - table per entity.
```sql
CREATE TABLE employees(
    id INTEGER,
    name TEXT,
    age INTEGER,
    is_manager BOOLEAN,
    salary INTEGER
);
```

Altering tables
```sql
-- rename tables
ALTER TABLE employees
RENAME TO contractors;

ALTER TABLE contractors
RENAME COLUMN salary TO invoice;

-- add a column
ALTER TABLE contractors
ADD COLUMN job_title TEXT;

-- drop a column
ALTER TABLE contractors
DROP COLUMN is_manager;
```

>[!info] What are migrations?
>It's a change to the structure of a relational database. You can think of it like a commit in Git, but for your database schema. Every migration records how the structure of your data evolves over time.
>
>Migrations are essential for adapting your database to changing requirements, fixing mistakes, and rolling out new features. In a team setting, migrations ensure everyone applies the same changes in the same order.

>[!tip] Up and down migration
>Create an `up.sql` file when you need to update the database. And create another file like `down.sql` which will revert the changes in the database.
>Use a **tool to migrate** databases.



