# Controller Setup

So far, we have setup model, repository, dto, mapper and service. \
Next, let's setup the controller.

## Step 1 Controller

1. create a package `com.lousing.patientservice.controller`
1. create a class named `PatientController`
1. annotate the class with `@RestController`
1. also annotate it with `@RequestMapping("/patients")`
1. declare and inject the `PatientService`

```java
package com.lousing.patientservice.controller;

import com.lousing.patientservice.dto.PatientResponseDTO;
import com.lousing.patientservice.service.PatientService;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
@RequestMapping("/patients")
public class PatientController {
    private final PatientService patientService;

    public PatientController(PatientService patientService) {
        this.patientService = patientService;
    }

    @GetMapping
    public ResponseEntity<List<PatientResponseDTO>> getPatients() {
        List<PatientResponseDTO> patients = patientService.getPatients();
        return ResponseEntity.ok().body(patients);
    }
}

```

Restart the application and hit `http://localhost:4000/patients` from bruno.
