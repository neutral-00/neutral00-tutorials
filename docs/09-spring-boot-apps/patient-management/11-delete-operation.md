# Delete Operation

So far, we have implemented get, create, update operations. \
Next, let's implement the delete operation

## Step 1 Update PatientService

- Add `deletePatient` method in `PatientService`

```java
public void deletePatient(UUID id) {
    Patient patient = patientRepository.findById(id).orElseThrow(()-> new PatientNotFoundException("Patient not found with id: " + id));
    patientRepository.delete(patient);
}
```

- Next update `PatientController` to call the above method

```java
@DeleteMapping("/{id}")
public ResponseEntity<Void> deletePatient(@PathVariable UUID id) {
    patientService.deletePatient(id);
    return ResponseEntity.noContent().build();
}
```

Now you can hit a DELETE api from bruno
