
## ❓ Why PostgreSQL?

* 💡 Open-source, powerful and enterprise-grade
* 💾 ACID-compliant for safe transactions
* 🧩 Extensible (custom data types, operators, functions)
* 📊 Full support for relational + NoSQL (JSONB)
* 🔄 MVCC (Multiversion Concurrency Control) for performance
* 🔒 Advanced security, partitioning, indexing, constraints

## ⏱️ When to Use PostgreSQL?

* Enterprise systems needing complex queries & high reliability
* Web apps (especially with ORMs like Hibernate, Sequelize)
* Geospatial applications (PostGIS)
* Systems with both structured and unstructured data (JSONB)

## ⚙️ What Makes It Different?

| Feature                  | PostgreSQL                      | MySQL          | Oracle DB  | MongoDB        |
| ------------------------ | ------------------------------- | -------------- | ---------- | -------------- |
| Type                     | Relational + Object             | Relational     | Relational | NoSQL Document |
| JSONB Support            | ✅ Yes                           | ⚠️ Basic JSON  | ❌          | ✅ Native       |
| ACID Compliance          | ✅ Full                          | ✅ Partial      | ✅ Full     | ⚠️ Not strict  |
| Partitioning             | ✅ Declarative & Flexible        | ✅ Manual setup | ✅          | ❌              |
| Full-Text Search         | ✅ Built-in                      | ⚠️ Limited     | ✅          | ✅              |
| Procedural Language (PL) | ✅ PL/pgSQL, PL/Python, etc.     | ❌ Stored Proc  | ✅ PL/SQL   | ❌              |
| Licensing                | PostgreSQL License (Permissive) | GPL            | Commercial | SSPL           |

---

### 🧾 PostgreSQL Data Types Explained

#### 1️⃣ Numeric Types

| Data Type          | Description                            | Example             |
| ------------------ | -------------------------------------- | ------------------- |
| `SMALLINT`         | 2 bytes integer (-32,768 to +32,767)   | 100                 |
| `INTEGER` or `INT` | 4 bytes integer (-2B to +2B)           | 100000              |
| `BIGINT`           | 8 bytes integer                        | 9223372036854775807 |
| `DECIMAL(p, s)`    | Exact numeric with precision and scale | 1234.56             |
| `NUMERIC(p, s)`    | Same as DECIMAL                        | 99.99               |
| `REAL`             | 4 bytes floating point                 | 3.14                |
| `DOUBLE PRECISION` | 8 bytes floating point                 | 3.1415926535        |

#### 2️⃣ Character Types

| Data Type    | Description            | Example                |
| ------------ | ---------------------- | ---------------------- |
| `CHAR(n)`    | Fixed-length string    | 'ABC   '               |
| `VARCHAR(n)` | Variable-length string | 'Hello World'          |
| `TEXT`       | Unlimited length text  | 'This is a large text' |

#### 3️⃣ Date/Time Types

| Data Type   | Description                | Example               |
| ----------- | -------------------------- | --------------------- |
| `DATE`      | Calendar date (YYYY-MM-DD) | '2025-08-04'          |
| `TIME`      | Time of day (HH\:MM\:SS)   | '14:30:00'            |
| `TIMESTAMP` | Date and time              | '2025-08-04 14:30:00' |
| `INTERVAL`  | Time span                  | '1 day 2 hours'       |

#### 4️⃣ Boolean Type

| Data Type | Description   | Example |
| --------- | ------------- | ------- |
| `BOOLEAN` | True or False | TRUE    |

#### 5️⃣ Geometric Types (Advanced)

| Data Type | Description         | Example     |
| --------- | ------------------- | ----------- |
| `POINT`   | A point in 2D space | '(1,2)'     |
| `LINE`    | Infinite line       | '{1,2,3}'   |
| `CIRCLE`  | Circle              | '<(3,4),5>' |

#### 6️⃣ Network Address Types

| Data Type | Description            | Example             |
| --------- | ---------------------- | ------------------- |
| `CIDR`    | IPv4/IPv6 networks     | '192.168.0.0/24'    |
| `INET`    | IPv4/IPv6 host address | '192.168.0.1'       |
| `MACADDR` | MAC address            | '08:00:2b:01:02:03' |

#### 7️⃣ JSON Types

| Data Type | Description          | Example           |
| --------- | -------------------- | ----------------- |
| `JSON`    | Text-based JSON      | '{"name":"John"}' |
| `JSONB`   | Binary JSON (faster) | '{"name":"John"}' |

#### 8️⃣ UUID

| Data Type | Description                   | Example                                |
| --------- | ----------------------------- | -------------------------------------- |
| `UUID`    | Universally Unique Identifier | 'a0eebc99-9c0b-4ef8-bb6d-6bb9bd380a11' |

### 🛠️ Example Table with Different Data Types

```sql
CREATE TABLE employee (
  emp_id UUID PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  salary NUMERIC(10,2),
  joining_date DATE,
  is_active BOOLEAN,
  profile JSONB
);
```

---

### 🏷️ PostgreSQL Constraints Explained

#### 1️⃣ NOT NULL

Ensures a column cannot have NULL value.

```sql
name VARCHAR(100) NOT NULL
```

#### 2️⃣ UNIQUE

Ensures all values in a column are unique.

```sql
email VARCHAR(100) UNIQUE
```

#### 3️⃣ PRIMARY KEY

Combination of NOT NULL + UNIQUE.

```sql
emp_id UUID PRIMARY KEY
```

#### 4️⃣ FOREIGN KEY

Ensures value exists in another table.

```sql
FOREIGN KEY (dept_id) REFERENCES department(dept_id)
```

#### 5️⃣ CHECK

Validates data based on condition.

```sql
age INT CHECK (age >= 18)
```

#### 6️⃣ DEFAULT

Sets default value if none provided.

```sql
is_active BOOLEAN DEFAULT TRUE
```

#### 7️⃣ EXCLUSION

Ensures rows do not overlap in some way (used with geometric types, ranges).

```sql
EXCLUDE USING gist (period WITH &&)
```

### 🛠️ Example Table with Constraints

```sql
CREATE TABLE department (
  dept_id SERIAL PRIMARY KEY,
  name VARCHAR(50) NOT NULL UNIQUE
);

CREATE TABLE employee (
  emp_id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE,
  age INT CHECK (age >= 18),
  dept_id INT REFERENCES department(dept_id),
  is_active BOOLEAN DEFAULT TRUE
);
```

---

## ✅ Summary

* **Data types** define the kind of data stored in columns.
* **Constraints** enforce rules on the data to maintain data integrity.
* Combining both ensures powerful and reliable database schema design.

---

### 🧾 CRUD Operation Breakdown

```sql
-- Insert data into table
INSERT INTO students (name, age) VALUES ('Alice', 20);
-- Adds a new student named Alice with age 20

-- Read data from table
SELECT * FROM students;
-- Retrieves all columns and rows from 'students'

-- Update data in table
UPDATE students SET age = 21 WHERE name = 'Alice';
-- Changes Alice's age to 21

-- Delete data from table
DELETE FROM students WHERE name = 'Alice';
-- Removes Alice's record from the table
```

---

### 🔗 Joins (Detailed)

#### ✅ INNER JOIN

Returns only the matching rows from both tables.

```sql
SELECT s.name, e.course_id
FROM students s
INNER JOIN enrollments e ON s.id = e.student_id;
```

* Fetches only students who are enrolled in a course.

#### ✅ LEFT JOIN (or LEFT OUTER JOIN)

Returns all rows from the left table, even if there's no match in the right table.

```sql
SELECT s.name, e.course_id
FROM students s
LEFT JOIN enrollments e ON s.id = e.student_id;
```

* Returns all students. If a student isn't enrolled, `course_id` will be NULL.

#### ✅ RIGHT JOIN (or RIGHT OUTER JOIN)

Returns all rows from the right table, even if there's no match in the left table.

```sql
SELECT s.name, e.course_id
FROM students s
RIGHT JOIN enrollments e ON s.id = e.student_id;
```

* Returns all enrollments. If no matching student, `name` will be NULL.

#### ✅ FULL JOIN (or FULL OUTER JOIN)

Returns rows when there is a match in either left or right table.

```sql
SELECT s.name, e.course_id
FROM students s
FULL JOIN enrollments e ON s.id = e.student_id;
```

* Returns all students and all enrollments, with NULLs where there's no match.

#### ✅ CROSS JOIN

Returns a Cartesian product — every row from the first table is paired with every row from the second.

```sql
SELECT s.name, c.name
FROM students s
CROSS JOIN courses c;
```

* Each student is paired with every course.

#### ✅ SELF JOIN

Join a table to itself using aliases.

```sql
SELECT a.name AS student1, b.name AS student2
FROM students a, students b
WHERE a.age = b.age AND a.id <> b.id;
```

* Finds pairs of students who have the same age.

---

### 📊 Visual Summary (Join Types)

| Join Type  | Includes Unmatched Left | Includes Unmatched Right | Only Matches |
| ---------- | ----------------------- | ------------------------ | ------------ |
| INNER JOIN | ❌                       | ❌                        | ✅            |
| LEFT JOIN  | ✅                       | ❌                        | ✅            |
| RIGHT JOIN | ❌                       | ✅                        | ✅            |
| FULL JOIN  | ✅                       | ✅                        | ✅            |
| CROSS JOIN | ✅ All combinations      | ✅ All combinations       | ❌            |

> 📘 Use `JOIN` wisely based on how much data you need and whether missing matches matter.

---
### 📌 Views (Detailed)

#### 📘 Where & Why to Use Views

* **Purpose:** To encapsulate complex queries into reusable, secure, and simplified structures.
* **When to Use:**

  * Hiding complexity from end users
  * Restricting access to specific columns (security)
  * Abstracting data for reporting
* **Why:** Views act like read-only tables but reduce redundancy and improve maintainability.

#### ✅ What is a View?

A **view** is a virtual table based on the result of a SQL query.

```sql
CREATE VIEW student_course_view AS
SELECT s.name, e.course_id
FROM students s
JOIN enrollments e ON s.id = e.student_id;
```

* Acts like a table but does not store data itself.
* Useful for abstraction, security, and simplifying complex queries.

```sql
SELECT * FROM student_course_view;
```

#### ✅ Updating Views

Some views are updatable:

```sql
UPDATE student_course_view SET course_id = 2 WHERE name = 'Alice';
```

> ⚠️ Works only if the view has a direct 1:1 mapping to the base table without aggregates or joins.

---

### 🛠️ Functions (Detailed)

#### 📘 Where & Why to Use Functions

* **Purpose:** Encapsulate logic for reuse, consistency, and encapsulation.
* **When to Use:**

  * When logic is repeated in multiple queries
  * For custom calculations or transformations
* **Why:** They reduce code duplication, and can be called inside SQL queries or triggers.

#### ✅ SQL Function

```sql
CREATE FUNCTION get_year(age INT) RETURNS INT AS $$
BEGIN
  RETURN EXTRACT(YEAR FROM CURRENT_DATE) - age;
END;
$$ LANGUAGE plpgsql;
```

* Accepts input and returns calculated output.
* `EXTRACT(YEAR FROM CURRENT_DATE)` gets current year.

#### ✅ Calling a Function

```sql
SELECT get_year(30); -- Output: e.g., 1993
```

---

### ⚙️ Triggers (Detailed)

#### 📘 Where & Why to Use Triggers

* **Purpose:** Automatically execute logic when a database event (INSERT, UPDATE, DELETE) occurs.
* **When to Use:**

  * Logging changes automatically
  * Enforcing business rules at DB level
  * Preventing invalid transactions
* **Why:** Helps enforce data integrity and system behavior without relying on app logic.

#### ✅ What is a Trigger?

* A **trigger** automatically executes a function in response to events on a table (INSERT, UPDATE, DELETE).

```sql
CREATE TABLE logs (
  id SERIAL PRIMARY KEY,
  message TEXT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE FUNCTION log_student_insert() RETURNS trigger AS $$
BEGIN
  INSERT INTO logs(message) VALUES ('New student added');
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_student_add
AFTER INSERT ON students
FOR EACH ROW EXECUTE FUNCTION log_student_insert();
```

* Automatically logs each student insert.

---

### ⚡ Indexes (Detailed)

#### 📘 Where & Why to Use Indexes

* **Purpose:** Speed up data retrieval operations.
* **When to Use:**

  * Columns used in WHERE, JOIN, or ORDER BY clauses
  * Large datasets with frequent read operations
* **Why:** Without indexes, PostgreSQL must scan entire tables (slow for big data). Indexes improve performance at the cost of slower writes.

#### ✅ What is an Index?

* Improves the speed of data retrieval.

```sql
CREATE INDEX idx_students_name ON students(name);
```

#### ✅ Unique Index

```sql
CREATE UNIQUE INDEX idx_unique_email ON students(email);
```

> 📌 Use `EXPLAIN ANALYZE` to see index effectiveness.

---

### 📦 Partitioning (Detailed)

#### 📘 Where & Why to Use Partitioning

* **Purpose:** Split large tables into smaller, manageable chunks based on key fields (e.g., date, ID).
* **When to Use:**

  * When working with very large tables (millions+ rows)
  * When older data is queried less frequently
* **Why:** Improves query performance and management. PostgreSQL can scan only relevant partitions instead of whole tables.

#### ✅ What is Partitioning?

* Splitting a large table into smaller pieces for performance.

```sql
CREATE TABLE measurements (
  id SERIAL,
  log_date DATE NOT NULL,
  temperature NUMERIC
) PARTITION BY RANGE (log_date);

CREATE TABLE measurements_2024 PARTITION OF measurements
  FOR VALUES FROM ('2024-01-01') TO ('2025-01-01');
```

* Queries on 2024 data hit only `measurements_2024`.

---

### 🧾 JSONB (Detailed)

#### 📘 Where & Why to Use JSONB

* **Purpose:** Store semi-structured data (like JSON documents) inside relational tables.
* **When to Use:**

  * When you need flexible schema (e.g., metadata, logs)
  * When values vary between rows
* **Why:** JSONB offers better performance and indexing than plain JSON and supports powerful querying via operators.

#### ✅ What is JSONB?

* A binary-encoded JSON format (faster than JSON).

```sql
CREATE TABLE products (
  id SERIAL,
  details JSONB
);

INSERT INTO products(details)
VALUES ('{"name": "Laptop", "price": 1500}');
```

#### ✅ JSONB Queries

```sql
SELECT * FROM products WHERE details ->> 'name' = 'Laptop';
```

* `->>` gets JSON field as text.

---

### 🔄 CTEs & 🪟 Window Functions (Detailed)

#### 📘 Where & Why to Use CTEs

* **Purpose:** Break down complex queries into readable, modular parts.
* **When to Use:**

  * With recursive queries
  * For debugging and better readability
* **Why:** CTEs simplify maintenance of complex SQL and support recursion.

#### 📘 Where & Why to Use Window Functions

* **Purpose:** Perform calculations across a window (subset) of rows related to the current row.
* **When to Use:**

  * Ranking, percentiles, moving averages
  * When you need row-wise operations without collapsing rows
* **Why:** Enables powerful analytics directly within SQL, no need for separate aggregation.

#### ✅ What is a CTE?

* A temporary result set referenced in a query.

```sql
WITH underage AS (
  SELECT * FROM students WHERE age < 18
)
SELECT * FROM underage;
```

---

### 🪟 Window Functions

#### ✅ What is a Window Function?

* Performs calculation across a set of rows related to the current row.

```sql
SELECT name, age,
  RANK() OVER (ORDER BY age DESC) AS age_rank
FROM students;
```

* `RANK()` assigns ranking without collapsing rows.

---

## 🧑‍🏫 Summary

* Views simplify queries
* Functions allow reusable business logic
* Triggers automate behavior
* Indexes boost speed
* Partitioning scales big data
* JSONB supports dynamic schemas
* CTEs improve query clarity
* Window functions power advanced analytics

---

## 🧪 Tooling & Monitoring

* `pgAdmin`: Web GUI for managing PostgreSQL.
* `DBeaver`: Universal SQL client.
* `EXPLAIN ANALYZE`: View query plan and performance.
* `pg_stat_statements`: Built-in extension for query analysis.
* `pg_dump` / `pg_restore`: Tools for backups and recovery.

---
