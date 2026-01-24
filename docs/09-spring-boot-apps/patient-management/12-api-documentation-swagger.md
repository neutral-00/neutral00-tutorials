# API Documentation - Swagger

Let's document the patient apis we created using swagger and open api.

## Reference

> [springdoc](https://springdoc.org)

## Steps

1. add the below dependency in `pom.xml`

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.8.15</version>
</dependency>

```

**CAUTION**

> I had to downgrade springboot version to 3.5.9 as it had compatibility issues

2. Add a tag to the `PatientController` as shown below

```java

@RestController
@RequestMapping("/patients")
@Tag(name = "Patient Management", description = "APIs for managing patients")
public class PatientController {
    // rest of the code
}
```

3. add the below annotation on `getPatients` method

```java
@GetMapping
@Operation(summary = "Get All Patients", description = "Retrieve a list of all patients")
public ResponseEntity<List<PatientResponseDTO>> getPatients() {
    List<PatientResponseDTO> patients = patientService.getPatients();
    return ResponseEntity.ok().body(patients);
}
```

Similary update the remaining methods \
Access the endpoint `http://server:port/context-path/swagger-ui.html`

In our project context it is `http://localhost:4000/swagger-ui/index.html`

Or if you want json format hit `http://localhost:4000/v3/api-docs`
