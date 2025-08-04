...\[Previous content preserved]...

---

# 🧪 Testing & Tooling – Detailed Guide (Beginner to Expert)

Testing ensures code correctness, maintainability, and confidence during development. Tooling enables automation, logging, and easier collaboration.

---

## 🔸 1. JUnit 5 Basics and Assertions (Unit Testing Framework)

JUnit 5 is the de facto standard testing framework in Java.

### ✅ Key Features:

* Annotation-based (`@Test`, `@BeforeEach`, etc.)
* Assertions for validating expected results
* Works with Maven/Gradle

### ✅ Example

```java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {

    @BeforeEach
    void setup() {
        // Code before each test
        System.out.println("Test setup");
    }

    @Test
    void testAddition() {
        int result = 2 + 3;
        assertEquals(5, result); // Output: true if 2+3==5
    }

    @Test
    void testBoolean() {
        assertTrue(10 > 5); // Output: true
    }

    @Test
    void testException() {
        assertThrows(ArithmeticException.class, () -> {
            int res = 1 / 0;
        });
    }
}
```

### ✅ Assertions Summary

* `assertEquals(expected, actual)`
* `assertTrue(condition)`
* `assertFalse(condition)`
* `assertThrows(Exception.class, ...)`

---

## 🔸 2. Mockito for Mocking (Dependency Isolation)

Mockito is used to create dummy (mock) objects for testing code that depends on external systems.

### ✅ Example: Mocking a List

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;
import java.util.List;

public class MockDemo {
    @Test
    void testMockList() {
        List<String> mockList = mock(List.class);

        when(mockList.get(0)).thenReturn("Mocked Item");
        assertEquals("Mocked Item", mockList.get(0)); // Output: Mocked Item

        verify(mockList).get(0); // Check if method was called
    }
}
```

### ✅ Why Mockito?

* Isolate dependencies
* Test logic independently
* Avoid hitting DB, network, etc.

---

## 🔸 3. Test-Driven Development (TDD)

### ✅ TDD Cycle:

1. Write a failing test
2. Write minimal code to pass
3. Refactor the code

### ✅ Example

```java
// Test First
@Test
void greetTest() {
    Greeter g = new Greeter();
    assertEquals("Hello, Alice", g.greet("Alice"));
}

// Implement Greeter
class Greeter {
    public String greet(String name) {
        return "Hello, " + name;
    }
}
```

TDD improves:

* Design
* Test coverage
* Confidence

---

## 🔸 4. Maven & Gradle (Build Tools)

Both tools manage dependencies, build lifecycle, testing, packaging, etc.

### ✅ Maven (XML-based)

```xml
<!-- pom.xml -->
<dependencies>
  <dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.9.0</version>
    <scope>test</scope>
  </dependency>
</dependencies>
```

**Commands:**

```bash
mvn test      # Runs test
mvn package   # Builds JAR/WAR
```

### ✅ Gradle (Groovy/Kotlin DSL)

```groovy
// build.gradle
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.9.0'
}
```

**Commands:**

```bash
gradle test     # Run tests
gradle build    # Build project
```

---

## 🔸 5. Logging (Debugging & Monitoring)

Logging records events or messages during execution. Logging levels:

* `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`

### ✅ SLF4J with Logback

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class LoggerDemo {
    private static final Logger log = LoggerFactory.getLogger(LoggerDemo.class);

    public static void main(String[] args) {
        log.info("Starting app...");
        log.error("Something failed!");
    }
}
```

### ✅ Log4j2 (Custom Configuration)

```xml
<!-- log4j2.xml -->
<Configuration>
  <Appenders>
    <Console name="Console" target="SYSTEM_OUT">
      <PatternLayout pattern="%d{HH:mm:ss} [%t] %-5level %logger - %msg%n"/>
    </Console>
  </Appenders>
  <Loggers>
    <Root level="info">
      <AppenderRef ref="Console"/>
    </Root>
  </Loggers>
</Configuration>
```

### ✅ Java Util Logging

```java
import java.util.logging.Logger;

public class BuiltInLoggerDemo {
    private static final Logger logger = Logger.getLogger("AppLogger");

    public static void main(String[] args) {
        logger.info("This is info");
    }
}
```

---

## ✅ Summary

| Concept      | Description                                       |
| ------------ | ------------------------------------------------- |
| JUnit 5      | Unit testing with annotations and assertions      |
| Mockito      | Mocking framework for isolating dependencies      |
| TDD          | Write tests before code to guide implementation   |
| Maven/Gradle | Build automation and dependency management        |
| Logging      | Track runtime behavior using SLF4J, Log4j, or JUL |

---

# 🧪 Full CRUD + Kafka Integration with Spring Boot, PostgreSQL, Kafka

## ✅ Tech Stack:

* Spring Boot
* PostgreSQL
* Apache Kafka
* JUnit 5
* Mockito
* Maven

---

## 🔸 1. Entity: User

```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;

    // Getters and Setters
}
```

---

## 🔸 2. Repository

```java
public interface UserRepository extends JpaRepository<User, Long> {}
```

---

## 🔸 3. Service with Kafka Producer

```java
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;
    @Autowired
    private KafkaTemplate<String, String> kafkaTemplate;

    private static final String TOPIC = "user-topic";

    public User createUser(User user) {
        User saved = userRepository.save(user);
        kafkaTemplate.send(TOPIC, "User created: " + saved.getId());
        return saved;
    }

    public Optional<User> getUser(Long id) {
        return userRepository.findById(id);
    }

    public List<User> getAllUsers() {
        return userRepository.findAll();
    }

    public void deleteUser(Long id) {
        userRepository.deleteById(id);
        kafkaTemplate.send(TOPIC, "User deleted: " + id);
    }
}
```

---

## 🔸 4. Kafka Consumer

```java
@Component
public class UserConsumer {
    @KafkaListener(topics = "user-topic", groupId = "group_id")
    public void consume(String message) {
        System.out.println("Consumed message: " + message);
    }
}
```

---

## 🔸 5. Controller

```java
@RestController
@RequestMapping("/users")
public class UserController {
    @Autowired
    private UserService userService;

    @PostMapping
    public ResponseEntity<User> create(@RequestBody User user) {
        return ResponseEntity.ok(userService.createUser(user));
    }

    @GetMapping("/{id}")
    public ResponseEntity<User> get(@PathVariable Long id) {
        return userService.getUser(id).map(ResponseEntity::ok)
            .orElse(ResponseEntity.notFound().build());
    }

    @GetMapping
    public List<User> list() {
        return userService.getAllUsers();
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> delete(@PathVariable Long id) {
        userService.deleteUser(id);
        return ResponseEntity.noContent().build();
    }
}
```

---

## 🔸 6. JUnit + Mockito Test

```java
@SpringBootTest
@ExtendWith(MockitoExtension.class)
class UserServiceTest {

    @InjectMocks
    private UserService userService;

    @Mock
    private UserRepository userRepository;

    @Mock
    private KafkaTemplate<String, String> kafkaTemplate;

    @Test
    void testCreateUser() {
        User user = new User();
        user.setName("Test User");
        user.setEmail("test@example.com");

        when(userRepository.save(any(User.class))).thenReturn(user);

        User saved = userService.createUser(user);

        assertEquals("Test User", saved.getName());
        verify(kafkaTemplate).send(anyString(), contains("User created"));
    }

    @Test
    void testDeleteUser() {
        doNothing().when(userRepository).deleteById(1L);
        userService.deleteUser(1L);
        verify(userRepository).deleteById(1L);
        verify(kafkaTemplate).send(anyString(), contains("User deleted"));
    }
}
```

---

## ✅ Summary

| Layer      | Component                              |
| ---------- | -------------------------------------- |
| Entity     | User                                   |
| Repository | UserRepository extends JpaRepository   |
| Service    | UserService + KafkaProducer            |
| Consumer   | KafkaListener for user-topic           |
| Controller | REST endpoints `/users`, `/users/{id}` |
| Test       | JUnit5 + Mockito                       |

---

## 🔸 7. Full Test Suite (JUnit + Mockito)

### ✅ 7.1 UserControllerTest

```java
@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void testCreateUser() throws Exception {
        User user = new User();
        user.setId(1L);
        user.setName("Test");
        user.setEmail("test@mail.com");

        when(userService.createUser(any(User.class))).thenReturn(user);

        mockMvc.perform(post("/users")
            .contentType(MediaType.APPLICATION_JSON)
            .content("{"name":"Test","email":"test@mail.com"}"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.id").value(1));
    }

    @Test
    void testGetUser() throws Exception {
        User user = new User();
        user.setId(1L);
        user.setName("Test");

        when(userService.getUser(1L)).thenReturn(Optional.of(user));

        mockMvc.perform(get("/users/1"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.name").value("Test"));
    }
}
```

### ✅ 7.2 UserRepositoryTest (Integration)

```java
@DataJpaTest
class UserRepositoryTest {

    @Autowired
    private TestEntityManager entityManager;

    @Autowired
    private UserRepository userRepository;

    @Test
    void testFindById() {
        User user = new User();
        user.setName("RepoTest");
        user.setEmail("repo@test.com");
        entityManager.persist(user);

        Optional<User> found = userRepository.findById(user.getId());
        assertTrue(found.isPresent());
        assertEquals("RepoTest", found.get().getName());
    }
}
```

### ✅ 7.3 UserModelTest

```java
class UserModelTest {
    @Test
    void testGettersSetters() {
        User user = new User();
        user.setId(10L);
        user.setName("John");
        user.setEmail("john@mail.com");

        assertEquals(10L, user.getId());
        assertEquals("John", user.getName());
        assertEquals("john@mail.com", user.getEmail());
    }
}
```

### ✅ 7.4 Kafka Producer (within Service already tested)

Tested through `UserServiceTest`:

* Verifies that `kafkaTemplate.send()` is called on create/delete.

For full Kafka integration test, a Kafka Testcontainer setup is recommended.

---
