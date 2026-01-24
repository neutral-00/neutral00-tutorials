# Create a Spring Boot App

This section shows several ways to create a new Spring Boot application using Spring Initializr (the official project generator) and how to import and run the generated project.

## Using the Spring Initializr Web UI

1. Open the Spring Initializr in your browser: https://start.spring.io
2. Choose the build system (`Maven` or `Gradle`), language (`Java`), and the Spring Boot version.
3. Set `Group` and `Artifact` values (e.g. `com.example` and `demo`).
4. Choose the Java version (e.g. `17`, `21`) and packaging (`Jar` or `War`).
5. Add dependencies (for example: `Spring Web`, `Spring Data JPA`, `Thymeleaf`, `Spring Security`).
6. Click **Generate** to download a zip file containing the project.

After download, unzip the archive and open the project in your IDE.

## Using the Spring Initializr API (curl / PowerShell)

You can generate a project programmatically. Example using `curl` (Linux/macOS) or PowerShell `Invoke-WebRequest` on Windows.

PowerShell example (Windows):

```powershell
# Example: generate a Maven + Java 17 project with Spring Web
$uri = 'https://start.spring.io/starter.zip'
$params = @{ dependencies = 'web'; type = 'maven-project'; language = 'java'; bootVersion = '3.2.0'; baseDir = 'demo'; javaVersion = '17' }
Invoke-WebRequest -Uri $uri -Method GET -Body $params -OutFile './demo.zip'
Expand-Archive -Path './demo.zip' -DestinationPath './demo'
```

Using `curl` (Linux/macOS):

```bash
curl "https://start.spring.io/starter.zip?type=maven-project&language=java&bootVersion=3.2.0&baseDir=demo&groupId=com.example&artifactId=demo&name=demo&packageName=com.example.demo&dependencies=web&javaVersion=17" -o demo.zip
unzip demo.zip -d demo
```

Change `bootVersion`, `javaVersion`, `dependencies`, and other query parameters as needed. See https://start.spring.io for all supported query parameters.

## Using the Spring CLI

If you have the Spring CLI installed, you can run:

```powershell
# PowerShell example
spring init --build maven --java-version 17 --dependencies web,data-jpa demo

# Create a Gradle project instead
spring init --build gradle --java-version 17 --dependencies web demo-gradle
```

The `spring init` command generates the project in the current directory.

## Importing into an IDE (IntelliJ / Eclipse / VS Code)

- IntelliJ IDEA: `File -> Open` and select the generated folder (or `Import Project` and choose the build file). IntelliJ will detect the build system and import accordingly.
- Eclipse / Spring Tools: `File -> Import -> Existing Maven/Gradle Project`.
- VS Code: Open the folder and use the Java/Gradle/Maven extensions to import and build.

## Running the generated project

The generated project contains wrapper scripts. From the project root:

PowerShell (Maven):
```powershell
.\mvnw spring-boot:run
```

PowerShell (Gradle):
```powershell
.\gradlew bootRun
```

Or build and run the produced artifact:

```powershell
.\mvnw -DskipTests package
java -jar target\demo-0.0.1-SNAPSHOT.jar
```

## Choosing dependencies and packaging

- Pick dependencies that match your use case (web, data, security, messaging, etc.).
- Choose `Jar` for most microservices; choose `War` if you need to deploy to an external servlet container.
- Select a Java version supported both by Spring Boot and your runtime environment.

## Minimal project structure (generated)

- `src/main/java/...` - application and source code
- `src/main/resources` - application.properties / application.yml and static/templates
- `pom.xml` or `build.gradle` - build configuration
- `mvnw`, `mvnw.cmd`, `gradlew`, `gradlew.bat` - build wrappers

## Quick tips

- Use `spring-boot-starter-web` for REST and MVC web applications.
- When you add JPA, include a database driver and configure `spring.datasource.*`.
- Prefer constructor injection for beans; the generated code often uses `@SpringBootApplication` and a main class with `SpringApplication.run(...)`.

---

Next steps: import the generated project into your preferred IDE and run the app using the wrapper script for a reproducible build.

