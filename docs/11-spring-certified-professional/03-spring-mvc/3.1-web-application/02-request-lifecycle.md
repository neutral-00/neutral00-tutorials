# REST Request Lifecycle

This page summarizes the HTTP/REST request lifecycle in Spring (exam-focused). It explains what happens from the moment the servlet container receives an HTTP request until a response is produced. Focus areas match common Spring Certified Professional exam topics.

## High-level overview

- Client sends HTTP request to the server (Tomcat, Jetty, Undertow).
- The Servlet container receives the request and routes it to the Spring `DispatcherServlet` (if mapped to `/` or another URL pattern).
- `DispatcherServlet` orchestrates request handling: it consults `HandlerMapping` to find a handler, invokes `HandlerAdapter` to execute the handler (controller), applies `HandlerInterceptor`s and `Filter`s, handles exceptions, and selects a `ViewResolver` (in MVC) or writes the serialized body (in REST).

## Key components and their roles

- `Servlet Container` (container-level): Receives raw HTTP request and dispatches to `DispatcherServlet`.
- `Filter` (javax/servlet.Filter / jakarta.servlet.Filter):
	- Runs before Spring MVC processing and after response generation.
	- Common uses: logging, CORS, security, request wrapping.
- `DispatcherServlet`:
	- Central front controller for Spring MVC.
	- Initializes and holds references to `HandlerMapping`, `HandlerAdapter`, `HandlerExceptionResolver`, `ViewResolver`s, and other components.
- `HandlerMapping`:
	- Finds an appropriate handler for the request (e.g., `RequestMappingHandlerMapping` for `@RequestMapping`/`@GetMapping`).
	- Considers URL, HTTP method, headers, consumes/produces, and media type.
- `HandlerAdapter`:
	- Adapts the handler to a uniform invocation mechanism (e.g., `RequestMappingHandlerAdapter` supports `@Controller`/`@RequestBody`/`@ResponseBody`).
- `Controller` / Handler method:
	- Business logic entry point. Handler methods can return `ModelAndView`, `ResponseEntity<T>`, `String` view name, or domain objects annotated with `@ResponseBody`.
	- Method parameter resolution uses `HandlerMethodArgumentResolver`s (e.g., `@RequestParam`, `@PathVariable`, `@RequestBody`, `HttpServletRequest`, `Principal`).
- `HandlerInterceptors`:
	- Allow pre- and post-processing around handler execution (`preHandle`, `postHandle`, `afterCompletion`). Useful for auth checks, timing, and logging.
- `HandlerExceptionResolver`:
	- Converts exceptions thrown by handlers into responses. Examples: `ResponseStatusExceptionResolver`, `ExceptionHandlerExceptionResolver` (for `@ExceptionHandler`), `DefaultHandlerExceptionResolver`.
- `HttpMessageConverter`s:
	- Responsible for reading request bodies (`@RequestBody`) and writing response bodies (`@ResponseBody`). Common converters: Jackson JSON, String, Form data.
- `ViewResolver`/View rendering (MVC):
	- For server-side rendering (Thymeleaf, JSP), `ViewResolver` selects a `View` which renders HTML.

## Typical synchronous flow (Spring MVC)

1. Servlet container receives HTTP request and creates `HttpServletRequest`/`HttpServletResponse`.
2. Request forwarded to `DispatcherServlet`.
3. `DispatcherServlet` applies `Filter`s (if present) and mapped `ServletRequestListener`s.
4. `HandlerMapping` selects a handler (controller method) based on request attributes.
5. `HandlerInterceptors.preHandle()` will be invoked (in registration order). If any returns `false`, handling stops.
6. `HandlerAdapter` prepares method arguments using `HandlerMethodArgumentResolver`s and invokes the handler method.
7. Handler executes business logic and returns a value.
8. `HandlerAdapter` uses `HttpMessageConverter`s to write the response body (for REST) or prepares `ModelAndView` for view rendering.
9. `HandlerInterceptors.postHandle()` runs (if handler executed successfully).
10. View rendering occurs (if applicable) or the response body is written directly.
11. `HandlerInterceptors.afterCompletion()` runs for cleanup.
12. `DispatcherServlet` commits the response; servlet container sends it to the client.

## Asynchronous request processing

- Spring supports async via `Callable`, `DeferredResult`, or reactive stacks (WebFlux).
- With `Callable`/`DeferredResult`, `DispatcherServlet` can release the request thread and handle the response later when the result is ready. Important for scaling and non-blocking IO.
- Key exam points: `DispatcherServlet` must be configured with async support; `@Async` is different (thread-pool for method execution).

## WebFlux (reactive) differences (brief)

- WebFlux uses `DispatcherHandler` and non-blocking, reactive types (`Mono`, `Flux`).
- No `HttpServletRequest`/`HttpServletResponse` blocking model — uses `ServerWebExchange`.
- Handler mappings and argument resolvers exist but are adapted for reactive types.

## Security and transactions

- `Filter`s often contain security logic (e.g., Spring Security's `FilterChainProxy`) and run before `DispatcherServlet`.
- Transactions typically start in service layer methods annotated with `@Transactional` and are independent from request lifecycle but commonly begin during handler execution and commit/rollback after handler completes.

## Exception handling strategies

- `@ExceptionHandler` in controllers or `@ControllerAdvice` to handle exceptions and return proper responses (HTTP status, body).
- `ResponseStatusException` and `ResponseStatusExceptionResolver` for quick status-based exceptions.
- Global error attributes and `ErrorController` (Spring Boot) also contribute to error responses.

## Important annotations & classes to remember for the exam

- `@Controller`, `@RestController`, `@RequestMapping`, `@GetMapping`, `@PostMapping`
- `@RequestBody`, `@ResponseBody`, `@ResponseStatus`, `@ExceptionHandler`, `@ControllerAdvice`
- `DispatcherServlet`, `RequestMappingHandlerMapping`, `RequestMappingHandlerAdapter`
- `HandlerInterceptor` (preHandle/postHandle/afterCompletion)
- `Filter` (servlet filter chain)
- `HttpMessageConverter` (Jackson `MappingJackson2HttpMessageConverter`)
- `DeferredResult`, `Callable`, `WebAsyncTask` for async

## Exam tips

- Know the order: Filters -> DispatcherServlet -> HandlerMapping -> Interceptors(pre) -> Handler -> Interceptors(post) -> View/MessageConversion -> Interceptors(afterCompletion).
- Be able to identify where `@RequestBody` is read (argument resolvers + message converters) and where `@ResponseBody` is written (message converters).
- Understand differences between servlet filters and Spring interceptors (filters are servlet-level and run before `DispatcherServlet`).
- Remember common exception handling mechanisms and priority of `@ExceptionHandler` vs `HandlerExceptionResolver`.
- For asynchronous processing, know that the request thread is released and the result is processed later; remember relevant types like `Callable` and `DeferredResult`.

---

References and further reading:

- Spring Framework Reference — Web MVC section
- Spring Boot Reference — error handling and embedded servlet container
- Official docs: https://docs.spring.io
