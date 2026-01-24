# Create a Controller

This page explains how to create controllers for RESTful endpoints with Spring, focusing on concepts and examples relevant to the Spring Certified Professional exam.

## Controller types

- `@Controller` — used for MVC controllers that typically return view names and rely on view resolvers (Thymeleaf, JSP).
- `@RestController` — shorthand for `@Controller` + `@ResponseBody`; handler return values are written directly to the response body (JSON/XML) using `HttpMessageConverter`s.

## Basic handler method anatomy

- `@RequestMapping` (class- or method-level) maps URL paths and can specify HTTP method via `method` attribute.
- Shortcut annotations: `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping`.
- Common method parameters resolved by Spring:
  - `@PathVariable` — extract values from URI path
  - `@RequestParam` — query parameters
  - `@RequestBody` — request body (converted by `HttpMessageConverter`)
  - `HttpServletRequest`, `HttpServletResponse`, `Principal`, `Locale`, `Pageable`, etc.
- Common return types:
  - Domain object (serialized with `@ResponseBody` or `@RestController`)
  - `ResponseEntity<T>` for status and headers control
  - `ModelAndView` or `String` for view names (MVC)

## Example: simple REST controller

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

	// GET /api/users
	@GetMapping
	public List<User> list() {
		return List.of(new User(1L, "Alice"));
	}

	// GET /api/users/{id}
	@GetMapping("/{id}")
	public ResponseEntity<User> get(@PathVariable Long id) {
		return ResponseEntity.ok(new User(id, "User"+id));
	}

	// POST /api/users
	@PostMapping
	@ResponseStatus(HttpStatus.CREATED)
	public User create(@RequestBody User user) {
		user.setId(42L);
		return user;
	}
}

// simple DTO
public record User(Long id, String name) {}
```

## Using `ResponseEntity` and status codes

`ResponseEntity<T>` gives full control over HTTP status, headers, and body. Use it for custom status codes or headers (e.g., `Location` after POST).

```java
return ResponseEntity.created(URI.create("/api/users/42")).body(createdUser);
```

## Content negotiation and `produces`/`consumes`

- Use `produces` and `consumes` on mapping annotations to restrict or advertise content types (e.g., `application/json`, `application/xml`).

```java
@PostMapping(consumes = MediaType.APPLICATION_JSON_VALUE, produces = MediaType.APPLICATION_JSON_VALUE)
```

## Exception handling

- Use `@ExceptionHandler` within a controller or `@ControllerAdvice` for global handling.
- Return `ResponseEntity` or annotate exception handler with `@ResponseStatus`.

Example `@ControllerAdvice`:

```java
@ControllerAdvice
public class GlobalExceptionHandler {

	@ExceptionHandler(EntityNotFoundException.class)
	public ResponseEntity<String> handleNotFound(EntityNotFoundException ex) {
		return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
	}
}
```

## Path variables vs request params

- `@PathVariable` is used for URI template variables: `/items/{id}`.
- `@RequestParam` is used for query parameters: `/items?page=2&size=10`.

## Validation

- Use JSR-380 annotations (`@Valid`, `@NotNull`, `@Size`, etc.) on request DTOs and `@RequestBody` to trigger validation.
- Handle `MethodArgumentNotValidException` in exception handlers to return 400 with validation errors.

## Example: CRUD controller (in-memory)

```java
@RestController
@RequestMapping("/api/books")
public class BookController {
	private final Map<Long, Book> store = new ConcurrentHashMap<>();
	private final AtomicLong idGen = new AtomicLong(1);

	@GetMapping
	public Collection<Book> all() { return store.values(); }

	@GetMapping("/{id}")
	public ResponseEntity<Book> get(@PathVariable Long id) {
		var b = store.get(id);
		return b == null ? ResponseEntity.notFound().build() : ResponseEntity.ok(b);
	}

	@PostMapping
	public ResponseEntity<Book> create(@RequestBody @Valid Book book) {
		long id = idGen.getAndIncrement();
		book.setId(id);
		store.put(id, book);
		return ResponseEntity.created(URI.create("/api/books/" + id)).body(book);
	}

	@PutMapping("/{id}")
	public ResponseEntity<Book> update(@PathVariable Long id, @RequestBody Book update) {
		if (!store.containsKey(id)) return ResponseEntity.notFound().build();
		update.setId(id);
		store.put(id, update);
		return ResponseEntity.ok(update);
	}

	@DeleteMapping("/{id}")
	@ResponseStatus(HttpStatus.NO_CONTENT)
	public void delete(@PathVariable Long id) { store.remove(id); }
}

public static class Book {
	private Long id;
	private String title;
	// getters/setters, constructors omitted for brevity
}
```

## Testing controllers

- Use `@WebMvcTest` for slice tests of controllers with mocked service beans.
- Use `MockMvc` or TestRestTemplate (in integration tests) to perform requests and assert responses.

## Exam tips (controller-related)

- Know the difference between `@Controller` and `@RestController`.
- Understand how `@RequestBody` and `@ResponseBody` interact with `HttpMessageConverter`s.
- Remember argument resolver precedence and common resolvable types.
- Know how to return different status codes (`@ResponseStatus`, `ResponseEntity`).
- Be familiar with validation flow and common exceptions (`MethodArgumentNotValidException`, `HttpMessageNotReadableException`).

---

References:
- Spring MVC: https://docs.spring.io/spring-framework/docs/current/reference/html/web.html
- Testing: https://docs.spring.io/spring-boot/docs/current/reference/html/spring-boot-features.html#boot-features-testing
