# Repository Implementation

Next we need to implement that interface we just created. Create a class called `StubSpeakerRepositoryImpl`. We are naming it this way because we are going to use stub data for now. Later we will interact with actual DB.

```java title="src/main/java/org/lousing/repository/StubSpeakerRepositoryImpl.java"
package org.lousing.repository;

import org.lousing.model.Speaker;

import java.util.ArrayList;
import java.util.List;

public class StubSpeakerRepositoryImpl {

    public List<Speaker> findAll() {
        List<Speaker> speakers = new ArrayList<>();
        Speaker speaker = new Speaker();
        speaker.setFirstName("Bryan");
        speaker.setLastName("Hansen");
        speakers.add(speaker);

        return speakers;
    }
}

```