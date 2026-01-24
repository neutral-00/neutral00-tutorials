# Post Request Setup

Next, let's update the `PatientService` to create a patient. \
Update it. Add the below method:

```java
public PatientResponseDTO createPatient(PatientRequestDTO requestDTO) {
    Patient newPatient =  patientRepository.save(PatientMapper.toModel(requestDTO));
    return PatientMapper.toDTO(newPatient);
}
```

Next update the `PatientController` \
Add the below method:

```java
@PostMapping
public ResponseEntity<PatientResponseDTO> createPatient(@Valid @RequestBody PatientRequestDTO patientRequestDTO) {
    PatientResponseDTO patientResponseDTO = patientService.createPatient(patientRequestDTO);
    return ResponseEntity.ok().body(patientResponseDTO);
}
```

Now you can hit a post request from bruno

```json
{
  "name": "John Doe",
  "email": "john.doe@email.com",
  "address": "123 main street",
  "dateOfBirth": "1990-02-01",
  "registeredDate": "2025-10-30"
}
```

Also you can check if the validations are working fine, pass an empty email and try the post request.
