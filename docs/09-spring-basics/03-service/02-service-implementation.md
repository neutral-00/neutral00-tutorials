# Service Implementation

We have defined a service interface, now let's implement it.

```java title="src/main/java/org/lousing/sevice/SpeakerServiceImpl.java"
package org.lousing.service;

import org.lousing.model.Speaker;
import org.lousing.repository.SpeakerRepository;
import org.lousing.repository.StubSpeakerRepositoryImpl;

import java.util.List;

public class SpeakerServiceImpl implements SpeakerService {

    private SpeakerRepository repository = new StubSpeakerRepositoryImpl();

    @Override
    public List<Speaker> findAll() {
        return repository.findAll();
    }

}

```