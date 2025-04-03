# Model Definition

We are going to store data related to conference speakers.
So let's create a model: `Speaker`

## Steps - Model Creation
1. Under `src/main/java` create a package `org.lousing.model`
2. Next inside it create the java class `Speaker`

```java title="src/main/java/org/lousing/model/Speaker.java"
package org.lousing.model;

public class Speaker {
    private String firstName;
    private String lastName;

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
}
```