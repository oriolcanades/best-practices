# Builder Pattern

El patrón Builder es un patrón de diseño creacional que nos permite construir objetos complejos paso a paso. El patrón nos permite producir diferentes tipos y representaciones de un objeto utilizando el mismo código de construcción.

```java
@Getter
@Setter
@Builder
public class User {
    private final String name;
    private final String email;
}
```

Para crear una instancia de la clase User, podemos usar el constructor de la clase o el patrón Builder:

```java
User user = User.builder()
        .name("John")
        .email("john@example")
        .build();
```
