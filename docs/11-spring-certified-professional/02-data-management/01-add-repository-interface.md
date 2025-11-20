# Repository Definition

Now that we have a model to hold our data, next we need a repository to persist data we hold in our model. Create an interface called `SpeakerRepository`.

```java title="src/main/java/org/lousing/repository/SpeakerRepository.java"
package org.lousing.repository;

import org.lousing.model.Speaker;

import java.util.List;

public interface SpeakerRepository {
    List<Speaker> findAll();
}

```