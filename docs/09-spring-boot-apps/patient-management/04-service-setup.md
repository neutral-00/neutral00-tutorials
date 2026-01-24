# Service Setup

So far, we have setup entity, in-memory database, repository. \
Now, let's setup the service layer.

## Step 1 Setup PatientDTO

1. create a package `com.lousing.patientservice.dto`
1. inside it, create a class `PatientDTO`

```java
package com.lousing.patientservice.dto;

public class PatientResponseDTO {
    private String id;
    private String name;
    private String email;
    private String address;
    private String dateOfBirth;

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getEmail() {
        return email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public String getDateOfBirth() {
        return dateOfBirth;
    }

    public void setDateOfBirth(String dateOfBirth) {
        this.dateOfBirth = dateOfBirth;
    }
}

```

## Step 2 Setup Mapper

1. create a package `com.lousing.patientservice.mapper`
1. inside it, create a class `PatientMapper`

```java
package com.lousing.patientservice.mapper;

import com.lousing.patientservice.dto.PatientResponseDTO;
import com.lousing.patientservice.model.Patient;

public class PatientMapper {
    public static PatientResponseDTO toDTO(Patient patient){
        PatientResponseDTO responseDTO = new PatientResponseDTO();
        responseDTO.setId(patient.getId().toString());
        responseDTO.setName(patient.getName());
        responseDTO.setEmail(patient.getEmail());
        responseDTO.setAddress(patient.getAddress());
        responseDTO.setDateOfBirth(patient.getDateOfBirth().toString());
        return responseDTO;
    }
}

```

## Step 3 Setup PatientService

1. create a package `com.lousing.patientservice.service`
1. Inside it, create a java class `PatientService`
1. Annotate the class with `@Service`
1. Declare a private variable to hold the `PatientRepository`
1. Inject it via the constructor
1. For now, let's have one method to fetch all patient data using the dto and mapper we just created

```java
package com.lousing.patientservice.service;

import com.lousing.patientservice.dto.PatientResponseDTO;
import com.lousing.patientservice.mapper.PatientMapper;
import com.lousing.patientservice.model.Patient;
import com.lousing.patientservice.repository.PatientRepository;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class PatientService {
    private PatientRepository patientRepository;

    public PatientService(PatientRepository patientRepository) {
        this.patientRepository = patientRepository;
    }

    public List<PatientResponseDTO> getPatients() {
        List<Patient> patients = patientRepository.findAll();
        return patients.stream()
                .map(PatientMapper::toDTO)
                .toList();
    }
}

```
