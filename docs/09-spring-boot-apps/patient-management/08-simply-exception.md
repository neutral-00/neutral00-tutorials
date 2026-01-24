# Simplify Exception

As you might have encountered in previous section, currently our post api \
is giving out a lot of info when an exception is occured.
Let's simplify it by creating a global exception handler

## Steps

1. create a package `com.lousing.patientservice.exception`
1. inside it, create a java class `GlobalExceptionHandler`
1. annotate it with `@ControllerAdvice`
1. create a public method that recieves `MethodArgumentNotValidException` and returns `ResponseEtity<Map<String, String>>`
1. annotate it with `@ExceptionHandler` as shown below

```java
package com.lousing.patientservice.exception;

import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.MethodArgumentNotValidException;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;

import java.util.HashMap;
import java.util.Map;

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(MethodArgumentNotValidException.class)
    public ResponseEntity<Map<String, String>> handleValidationExceptions(MethodArgumentNotValidException ex) {
        Map<String, String> errors = new HashMap<>();
        ex.getBindingResult().getFieldErrors().forEach(error ->
            errors.put(error.getField(), error.getDefaultMessage()));
        return ResponseEntity.badRequest().body(errors);
    }
}

```

Try hitting the post request with similar payload as below:

```json
{
  "name": "John Doe",
  "email": "",
  "address": "",
  "dateOfBirth": "1990-02-01",
  "registeredDate": "2025-10-30"
}
```

You should see a simplified response
