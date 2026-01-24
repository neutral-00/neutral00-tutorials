# Enhance Validation

Next, let's enhance the validation for email field. \
Let's check if an email already exist before creating a patient.

## Steps

1. Update `PatientRepository`, add the below method

```java
package com.lousing.patientservice.repository;

import com.lousing.patientservice.model.Patient;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import java.util.UUID;

@Repository
public interface PatientRepository extends JpaRepository<Patient, UUID> {
    boolean existsByEmail(String email);
}

```

2. Next Create a custom exception handler

- Create a class `com.lousing.patientservice.exception.EmailAlreadyExistsException`

```java
package com.lousing.patientservice.exception;

public class EmailAlreadyExistsException extends RuntimeException {
    public EmailAlreadyExistsException(String message) {
        super(message);
    }
}
```

3. Next update the `PatientService>createPatient` method to throw the above exception if email already exists

```java
public PatientResponseDTO createPatient(PatientRequestDTO requestDTO) {
    if (patientRepository.existsByEmail(requestDTO.getEmail())) {
        throw new EmailAlreadyExistsException("A patient with this Email already exists: " + requestDTO.getEmail());
    }
    Patient newPatient = patientRepository.save(PatientMapper.toModel(requestDTO));
    return PatientMapper.toDTO(newPatient);
}
```

4. Update the `GlobalExcpetionHandler` class, add the below method

```java
@ExceptionHandler(EmailAlreadyExistsException.class)
public ResponseEntity<Map<String, String>> handleEmailAlreadyExistsException(EmailAlreadyExistsException ex) {
    log.warn("EmailAlreadyExistsException: {}", ex.getMessage());
    Map<String, String> error = new HashMap<>();
    error.put("message", "Email already exists");
    return ResponseEntity.badRequest().body(error);
}
```

Note that we have used `slf4j` logger

5. Finally in `application.properties` add the below entry

```
logging.level.root=INFO
```

Now in bruno, try to create a patient with an existing email. \
You should get the exception message as configured above.
