# DTO Pattern

<!-- TOC -->
* [DTO Pattern](#dto-pattern)
  * [Introducción](#introducción)
  * [Usando DTO, la necesidad de un Mapper](#usando-dto-la-necesidad-de-un-mapper)
  * [Usando DTO en la capa de servicio. DTO vs. Entity](#usando-dto-en-la-capa-de-servicio-dto-vs-entity)
<!-- TOC -->

## Introducción

Desde Java 14, podemos usar las clases de tipo record para crear un DTO. Un DTO es un objeto que se utiliza para transferir datos entre diferentes capas de una aplicación. Por ejemplo, entre la capa de presentación y la capa de servicio. Veamos un ejemplo:

```java
@Builder
public record UserDto(String name, String email) {}
```

En este ejemplo, hemos creado un DTO para representar un usuario. El DTO tiene dos propiedades: name y email. Podemos crear una instancia de este DTO de la siguiente manera:

```java
UserDto userDto = UserDto.builder().name("John").email("john@example.es").build();
```

## Usando DTO, la necesidad de un Mapper

Al trabajar con DTO necesitaremos usar un mapper para convertir un DTO en una entidad y viceversa. Para ello, podemos crear un Mapper. Veamos un ejemplo:

Custom Mapper:
```java
public class UserMapper {
    
    public User toEntity(UserDto userDto) {
        return User.builder()
                .name(userDto.getName())
                .email(userDto.getEmail())
                .build();
    }

    public UserDto toDto(User user) {
        return UserDto.builder()
                .name(user.getName())
                .email(user.getEmail())
                .build();
    }
    
}
```

También podemos usar MapStruct para generar el mapper. Mapstruct es una librería que nos permite generar código para mapear objetos. Para ello, necesitamos crear una interfaz con los métodos que necesitamos. Veamos un ejemplo:

```java
@Mapper
public interface UserMapper {
    
    UserMapper INSTANCE = Mappers.getMapper(UserMapper.class);
    
    User toEntity(UserDto userDto);
    
    UserDto toDto(User user);
    
}
```

Para generar el código, necesitamos añadir la siguiente dependencia a nuestro proyecto:

Gradle
```gradle
implementation 'org.mapstruct:mapstruct:1.4.2.Final'
```

Maven
```xml
<dependency>
    <groupId>org.mapstruct</groupId>
    <artifactId>mapstruct</artifactId>
    <version>1.4.2.Final</version>
</dependency>
```

**Nota**: A veces Mapstruck puede dar algún problema con Lombok. Para solucionarlo, podemos añadir la siguiente dependencia:

Gradle
```gradle
annotationProcessor 'org.projectlombok:lombok-mapstruct-binding:0.2.0'
```

Maven
```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok-mapstruct-binding</artifactId>
    <version>0.2.0</version>    
</dependency>
```

## Usando DTO en la capa de servicio. DTO vs. Entity

Los DTO son muy útiles para transferir datos entre diferentes capas de una aplicación. Las entidades, en cambio, son útiles para representar datos en la capa de persistencia. Por ejemplo, en una base de datos y por ello, no se deberían usar fuera de la capa de servicio o de persistencia. Vea el siguiente ejemplo:

```java
import org.w3c.dom.UserDataHandler;

@Service
@RequiredArgsConstructor
public class UserService {

    private final UserRepository userRepository;
    private final UserMapper userMapper;

    public UserDto createUser(UserDto userDto) {
        // Convert DTO to JPA Entity
        User user = userMapper.toEntity(userDto);
        
        User savedUser = userRepository.save(user);
        
        // Convert JPA Entity to DTO
        return userMapper.toDto(savedUser);
    }

}
```

De esta manera, la capa de servicio no expone las entidades de la capa de persistencia. En su lugar, expone DTO que son objetos simples que contienen datos.
