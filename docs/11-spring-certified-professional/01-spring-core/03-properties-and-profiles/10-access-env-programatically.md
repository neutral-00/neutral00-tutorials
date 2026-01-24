# Access Environment Programatically


1. Create a new REST controller named `EnvController.java` in the `com.lousing.poc.controller` package.
2. Inject the `Environment` object using `@Autowired`.
3. Create a method named `logActiveProfiles()` that handles.
4. Annotate this method with `@PostConstruct` to log the active profiles when the application starts.
5. In the method handling this endpoint, retrieve the active profiles from the `Environment` object and log them.
