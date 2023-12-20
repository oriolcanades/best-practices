# Error Handling

El manejo de errores es una parte fundamental de cualquier aplicación. En este apartado veremos cómo manejar los errores
en una API RESTful.

## Custom Error Response

Para devolver una respuesta de error personalizada, debemos crear una clase que contenga los datos que queremos devolver
en la respuesta de error.

```java

@Builder
public record ErrorDetails(LocalDateTime timestamp, String message, String details) {
}
```

## Global Exception Handler

El handler de excepciones global es un componente que se encarga de capturar todas las excepciones que se produzcan en
la aplicación y de devolver una respuesta HTTP con el código de error correspondiente.

Para ello, debemos crear una clase anotada con `@RestControllerAdvice` y añadir un método anotado
con `@ExceptionHandler` para cada tipo de excepción que queramos manejar.

```java

@Slf4j
@RestControllerAdvice
public class GlobalExceptionHandler extends ResponseEntityExceptionHandler {

    @ExceptionHandler(NotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public void handleNotFoundException() {
        log.error("NotFoundException");
    }

    @ExceptionHandler(Exception.class)
    @ResponseStatus(HttpStatus.SERVER_ERROR)
    public final ResponseEntity<ErrorResponse> handleAllExceptions(Exception ex, WebRequest request) {
        ErrorDetails errorDetails = ErrorDetails.builder()
                .localDate(LocalDateTime.now())
                .message(ex.getMessage())
                .details(request.getDescription(false))
                .build();
        return new ResponseEntity<>(errorDetails, HttpStatus.INTERNAL_SERVER_ERROR);
    }

    // ...
}
```

En el ejemplo anterior, se capturan las excepciones `NotFoundException` y `InvalidRequestException` y se devuelve un
error 404 Not Found y un error 400 Bad Request respectivamente.

## Custom Exceptions

Para crear una excepción personalizada, debemos crear una clase que extienda de `RuntimeException` y añadir un
constructor que reciba un mensaje de error.

```java
public class NotFoundException extends RuntimeException {

    public NotFoundException(String message) {
        super(message);
    }

    public NotFoundException(String message, Throwable cause) {
        super(message, cause);
    }

}
```


