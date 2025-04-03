# Service - Usage

Let's use the service to get data. Rename or create `Application.java` containing the `main` method.

```java title="src/main/java/org/lousing/Application.java"
package org.lousing;

import org.lousing.service.SpeakerService;
import org.lousing.service.SpeakerServiceImpl;

public class Application {
    public static void main(String[] args) {
        SpeakerService service = new SpeakerServiceImpl();
        System.out.println(service.findAll().getFirst().getFirstName());
    }
}
```