# Repository Setup

Previously we setup the entity and h2 in-memory database configuration. \
Next, let's setup the repository to interface the crud operations.

## Step 1 Define PatientRepository Interface

1. Create a package `com.louing.patientservice.repository`
2. In it, create an interface `PatientRepository`
3. Annotate the interface with `@Repository`
4. Next, extend the `JpaRepository` as shown below

```java
package com.lousing.patientservice.repository;

import com.lousing.patientservice.model.Patient;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import java.util.UUID;

@Repository
public interface PatientRepository extends JpaRepository<Patient, UUID> {
}

```

By extending from JpaRepository, we get a number of methods which will help perform CRUD.
