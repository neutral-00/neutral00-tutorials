# Update Patient Operation

So far, we have implemented get and post operation for patient. \
Next, let's implement the update operation.

## Steps 1 Create a ValidationGroup

- We will need to create a validation group to have some different validation behavior
- when we do and patient and update patient
- While performing add operation we want the RegisteredDate to be mandatory but ommitted while update
- To achieve this create an interface `com.lousing.patientservice.dto.validators.CreatePatientValidationGroup`

```java
package com.lousing.patientservice.dto.validators;

public interface CreatePatientValidationGroup {
}

```

- Next update the `PatientRequestDTO` registeredDate field as below

```java
@NotNull(groups = CreatePatientValidationGroup.class, message = "Registered Date is mandatory")
private String registeredDate;
```

- Next update `PatientController`'s createPatient and updatePatient methods as below

```java
@PostMapping
public ResponseEntity<PatientResponseDTO> createPatient(@Validated({Default.class, CreatePatientValidationGroup.class}) @RequestBody PatientRequestDTO patientRequestDTO) {
    PatientResponseDTO patientResponseDTO = patientService.createPatient(patientRequestDTO);
    return ResponseEntity.ok().body(patientResponseDTO);
}

@PutMapping("/{id}")
public ResponseEntity<PatientResponseDTO> updatePatient(@PathVariable UUID id, @Validated({Default.class}) @RequestBody PatientRequestDTO patientRequestDTO) {
    PatientResponseDTO patientResponseDTO = patientService.updatePatient(id, patientRequestDTO);
    return ResponseEntity.ok().body(patientResponseDTO);
}
```

- Next, let's handle how to update email. Update `PatientRepository` as below

```java
package com.lousing.patientservice.repository;

import com.lousing.patientservice.model.Patient;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import java.util.UUID;

@Repository
public interface PatientRepository extends JpaRepository<Patient, UUID> {
    boolean existsByEmail(String email);
    boolean existsByEmailAndIdNot(String email, UUID id);
}

```

- Next add the below method in the `PatientService`

```java
public PatientResponseDTO updatePatient(UUID id, PatientRequestDTO requestDTO) {
    Patient patient = patientRepository.findById(id).orElseThrow(()-> new PatientNotFoundException("Patient not found with id: " + id));
    // check if email is taken by another patient | or in other words, check if email exists for another patient id
    if (patientRepository.existsByEmailAndIdNot(requestDTO.getEmail(), id)) {
        throw new EmailAlreadyExistsException("A patient with this Email already exists: " + requestDTO.getEmail());
    }

    patient.setName(requestDTO.getName());
    patient.setEmail(requestDTO.getEmail());
    patient.setAddress(requestDTO.getAddress());
    patient.setDateOfBirth(java.time.LocalDate.parse(requestDTO.getDateOfBirth()));
    Patient updatedPatient = patientRepository.save(patient);
    return PatientMapper.toDTO(updatedPatient);
}
```

- Create the custom exception `PatientNotFoundException` in `com.lousing.patientserver.exception`

```java
package com.lousing.patientservice.exception;

public class PatientNotFoundException extends RuntimeException {
    public PatientNotFoundException(String message) {
        super(message);
    }
}

```

- Update `GlobalExceptionHandler`, add another method

```java
@ExceptionHandler(PatientNotFoundException.class)
public ResponseEntity<Map<String, String>> handlePatientNotFoundException(PatientNotFoundException ex) {
    log.warn("PatientNotFoundException: {}", ex.getMessage());
    Map<String, String> error = new HashMap<>();
    error.put("message", "Patient not found");
    return ResponseEntity.status(404).body(error);
}
```

Now you can test the update operations excluding the `registeredDate` field

- try updating some other fields keeping the same email
- try updating the email only
