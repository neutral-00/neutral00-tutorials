# Service Definition

We have a model to hold our data, and a repository to persist data. Next we need a service to interact with the repository. Let's create a service interface called SpeakerService

```java title="src/main/java/org/lousing/service/SpeakerService.java"
package org.lousing.service;

import org.lousing.model.Speaker;

import java.util.List;

public interface SpeakerService {
    List<Speaker> findAll();
}

```