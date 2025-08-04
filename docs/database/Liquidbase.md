# 📦 Liquibase + PostgreSQL + Partman Integration Guide

---

## ✅ What is Liquibase?

Liquibase is an open-source **database schema change management tool**.  
It tracks, manages, and applies database changes across environments safely and automatically.

---

## ✅ Why Use Liquibase?

- Version control for your DB schema  
- Keep dev/test/prod databases in sync  
- Works well with CI/CD pipelines  
- Supports YAML, XML, JSON, SQL formats  

---

## ✅ Key Terms

- **ChangeSet**: Single unit of change (e.g., create table)  
- **ChangeLog**: File containing a list of ChangeSets  
- **liquibase.properties**: Configuration (DB URL, credentials, changelog file)  

---

## ✅ Basic YAML ChangeSet

```yaml
- changeSet:
    id: 1
    author: darshan
    changes:
      - createTable:
          tableName: student
          columns:
            - column:
                name: id
                type: SERIAL
                constraints:
                  primaryKey: true
            - column:
                name: name
                type: VARCHAR(100)
```

Run:
```bash
liquibase update
```

---

## ✅ Rollback Support

```yaml
- changeSet:
    id: 2
    author: darshan
    changes:
      - addColumn:
          tableName: student
          columns:
            - column:
                name: age
                type: INT
    rollback:
      - dropColumn:
          columnName: age
          tableName: student
```

```bash
liquibase rollbackCount 1
```

---

## ✅ Preconditions

```yaml
preConditions:
  - not:
      - tableExists:
          tableName: student
```

---

## ✅ Tags & Snapshots

```bash
liquibase tag v1.0
liquibase snapshot
```

---

## ✅ Contexts (Environment Specific)

```yaml
- changeSet:
    id: 3
    author: darshan
    context: dev,test
    changes:
      - insert:
          tableName: student
          columns:
            - column: { name: name, value: 'test user' }
```

Run:
```bash
liquibase update --contexts=dev
```

---

## ✅ Modular ChangeLogs

```yaml
databaseChangeLog:
  - include:
      file: tables/student.yaml
  - include:
      file: data/init_data.yaml
```

---

## ✅ CI/CD Integration (GitHub Actions)

```yaml
- uses: liquibase/liquibase-github-action@v4.23.0
  with:
    operation: update
    changelogFile: changelog.yaml
```

---

## ☕ Liquibase + Spring Boot Setup (Maven)

### Step 1: Add Dependency

```xml
<dependency>
  <groupId>org.liquibase</groupId>
  <artifactId>liquibase-core</artifactId>
</dependency>
```

---

### Step 2: `db.changelog-master.yaml`

```yaml
databaseChangeLog:
  - include:
      file: db/changelog/001-create-student.yaml
```

---

### Step 3: Create ChangeSet File

`db/changelog/001-create-student.yaml`

```yaml
- changeSet:
    id: 001
    author: darshan
    changes:
      - createTable:
          tableName: student
          columns:
            - column:
                name: id
                type: BIGINT
                autoIncrement: true
                constraints:
                  primaryKey: true
            - column:
                name: name
                type: VARCHAR(100)
```

---

### Step 4: application.yml

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/yourdb
    username: youruser
    password: yourpass
  liquibase:
    change-log: classpath:/db/changelog/db.changelog-master.yaml
    enabled: true
```

---

### Step 5: Run

Liquibase auto-executes on Spring Boot start.  
For CLI:

```bash
mvn liquibase:update
```

Rollback:

```bash
mvn liquibase:rollback -Dliquibase.rollbackCount=1
```

---

## 📦 PostgreSQL Partman + Liquibase Integration

---

## ✅ What is pg_partman?

pg_partman is a PostgreSQL extension for **automated time-based or ID-based partitioning**.

---

## ✅ Step 1: Create Extension (Optional via Liquibase)

```yaml
- changeSet:
    id: 000
    author: darshan
    changes:
      - sql:
          sql: CREATE EXTENSION IF NOT EXISTS pg_partman;
```

Or manually:

```sql
CREATE EXTENSION IF NOT EXISTS pg_partman;
```

---

## ✅ Step 2: Create Parent Table with Partman

`001-create-events-parent.yaml`

```yaml
- changeSet:
    id: 001
    author: darshan
    changes:
      - sql:
          splitStatements: false
          sql: |
            CREATE TABLE IF NOT EXISTS public.events (
              id BIGSERIAL PRIMARY KEY,
              user_id INT NOT NULL,
              created_at TIMESTAMP NOT NULL,
              event_type TEXT NOT NULL
            ) PARTITION BY RANGE (created_at);
```

---

## ✅ Step 3: Register Table in pg_partman

`002-register-with-partman.yaml`

```yaml
- changeSet:
    id: 002
    author: darshan
    changes:
      - sql:
          splitStatements: false
          sql: |
            SELECT partman.create_parent(
              p_parent_table := 'public.events',
              p_control := 'created_at',
              p_type := 'native',
              p_interval := 'monthly',
              p_premake := 4
            );
```

---

## ✅ Step 4: Insert Sample Data (Optional)

```yaml
- changeSet:
    id: 003
    author: darshan
    context: dev
    changes:
      - insert:
          tableName: events
          columns:
            - column: { name: user_id, value: 101 }
            - column: { name: created_at, valueDate: "2025-08-01T00:00:00" }
            - column: { name: event_type, value: "login" }
```

---

## ✅ Step 5: Run Partman Maintenance

Required to pre-create partitions.

```sql
SELECT partman.run_maintenance();
```

Or via Liquibase:

```yaml
- changeSet:
    id: 004
    author: darshan
    changes:
      - sql:
          sql: SELECT partman.run_maintenance();
```

---

## ✅ Automate Maintenance via Cron or K8s Job

```bash
psql -U user -d yourdb -c "SELECT partman.run_maintenance();"
```

Or use a Kubernetes CronJob to automate this.

---

## ✅ Summary

| Component           | Details                                  |
|--------------------|-------------------------------------------|
| DB Change Tool     | Liquibase                                 |
| Partition Engine   | pg_partman                                |
| Partition Type     | RANGE (time-based: monthly)               |
| Maintenance        | `partman.run_maintenance()`               |
| DevOps Integration | GitHub Actions / Jenkins / CI/CD pipelines |
| Spring Boot        | Auto Liquibase changelog execution        |

---

✅ **You're now ready to use Liquibase with PostgreSQL Partman in microservices or monolithic apps!**

# 📦 Spring Boot + Liquibase + PostgreSQL Setup Guide

---

## ✅ Phase 1: Spring Boot + Liquibase + PostgreSQL (No Partitioning)

This section shows how to create a Spring Boot application with PostgreSQL and integrate Liquibase to manage schema changes.

---

### 🔹 Step 1: Spring Boot Project Setup

1. Go to [https://start.spring.io](https://start.spring.io)
2. Choose:

   * Project: Maven
   * Language: Java
   * Spring Boot: 3.x
   * Dependencies:

     * Spring Web
     * Spring Data JPA
     * PostgreSQL Driver
     * Liquibase

---

### 🔹 Step 2: application.yml

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/mydb
    username: postgres
    password: postgres
  jpa:
    hibernate:
      ddl-auto: none
  liquibase:
    enabled: true
    change-log: classpath:/db/changelog/db.changelog-master.yaml
```

---

### 🔹 Step 3: Create Liquibase Changelog

📁 `src/main/resources/db/changelog/db.changelog-master.yaml`

```yaml
databaseChangeLog:
  - include:
      file: db/changelog/001-create-user.yaml
```

📁 `src/main/resources/db/changelog/001-create-user.yaml`

```yaml
- changeSet:
    id: 001
    author: darshan
    changes:
      - createTable:
          tableName: user
          columns:
            - column:
                name: id
                type: BIGINT
                autoIncrement: true
                constraints:
                  primaryKey: true
            - column:
                name: name
                type: VARCHAR(100)
            - column:
                name: email
                type: VARCHAR(100)
            - column:
                name: role
                type: VARCHAR(50)
```

---

### 🔹 Step 4: Java Code for CRUD

#### `User.java`

```java
@Entity
public class User {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;
  private String name;
  private String email;
  private String role;
  // Getters & Setters
}
```

#### `UserRepository.java`

```java
public interface UserRepository extends JpaRepository<User, Long> {}
```

#### `UserService.java`

```java
@Service
public class UserService {
  @Autowired
  private UserRepository repository;

  public List<User> getAll() { return repository.findAll(); }
  public User getById(Long id) { return repository.findById(id).orElse(null); }
  public User save(User user) { return repository.save(user); }
  public void delete(Long id) { repository.deleteById(id); }
}
```

#### `UserController.java`

```java
@RestController
@RequestMapping("/api/users")
public class UserController {
  @Autowired
  private UserService service;

  @GetMapping public List<User> getAll() { return service.getAll(); }
  @GetMapping("/{id}") public User get(@PathVariable Long id) { return service.getById(id); }
  @PostMapping public User create(@RequestBody User u) { return service.save(u); }
  @PutMapping("/{id}") public User update(@PathVariable Long id, @RequestBody User u) {
    u.setId(id); return service.save(u);
  }
  @DeleteMapping("/{id}") public void delete(@PathVariable Long id) { service.delete(id); }
}
```

---

## ✅ Phase 2: Add pg\_partman for Partitioning

This section extends the base setup to use **pg\_partman** to manage PostgreSQL time-based partitions using Liquibase.

---

### 🔹 Step 1: Enable pg\_partman Extension

📁 `db/changelog/000-enable-extension.yaml`

```yaml
- changeSet:
    id: 000
    author: darshan
    changes:
      - sql:
          sql: CREATE EXTENSION IF NOT EXISTS pg_partman;
```

Include in master:

```yaml
  - include:
      file: db/changelog/000-enable-extension.yaml
```

---

### 🔹 Step 2: Create Partitioned Table

📁 `001-create-events-parent.yaml`

```yaml
- changeSet:
    id: 001
    author: darshan
    changes:
      - sql:
          splitStatements: false
          sql: |
            CREATE TABLE IF NOT EXISTS public.events (
              id BIGSERIAL PRIMARY KEY,
              user_id INT NOT NULL,
              created_at TIMESTAMP NOT NULL,
              event_type TEXT NOT NULL
            ) PARTITION BY RANGE (created_at);
```

---

### 🔹 Step 3: Register with pg\_partman

📁 `002-register-partman.yaml`

```yaml
- changeSet:
    id: 002
    author: darshan
    changes:
      - sql:
          sql: |
            SELECT partman.create_parent(
              p_parent_table := 'public.events',
              p_control := 'created_at',
              p_type := 'native',
              p_interval := 'monthly',
              p_premake := 4
            );
```

---

### 🔹 Step 4: Run Maintenance

📁 `004-run-maintenance.yaml`

```yaml
- changeSet:
    id: 004
    author: darshan
    changes:
      - sql:
          sql: SELECT partman.run_maintenance();
```

Schedule with Linux Cron or Kubernetes CronJob.

---

✅ You're now running a **Spring Boot + PostgreSQL + Liquibase + Partman** setup with versioned partitioning, auto-maintenance, and RESTful CRUD for users.
