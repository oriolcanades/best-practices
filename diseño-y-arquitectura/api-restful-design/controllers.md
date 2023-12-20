## Controllers

Los controladores no deben contener lógica de negocio, solo deben ser responsables de recibir las peticiones HTTP, validar los datos de entrada y delegar la ejecución a los servicios.

### @RestController

Los controladores deben ser anotados con `@RestController` para indicar que se trata de un controlador REST.

```java
@RestController
public class UserController {
    // ...
}
```

### @RequiredArgsConstructor

Como hemos visto en otros apartados, la inyección de dependencias se realiza mediante constructores, por lo que debemos declarar un constructor que reciba las dependencias necesarias. Podemos utilizar la anotación `@RequiredArgsConstructor` de Lombok para generar el constructor automáticamente.

```java
@RestController
@RequiredArgsConstructor
public class UserController {
    
    private final UserService userService;
    
    // ...
}
```

### @RequestMapping

La anotación `@RequestMapping` se utiliza para mapear una petición HTTP a un método del controlador. Se puede utilizar a nivel de clase y/o a nivel de método, pero nosotros recomendamos utilizarla a nivel de clase para indicar el prefijo de la ruta y a nivel de método usaremos otras anotaciones más específicas como `@GetMapping`, `@PostMapping`, `@PutMapping`, `@PatchMapping` y `@DeleteMapping`.

```java
@RestController
@RequiredArgsConstructor
@RequestMapping("/users")
public class UserController {
    
    private final UserService userService;
    
    @GetMapping
    public List<User> findAll() {
        return userService.findAll();
    }
    
    // ...
}
```

Es importante destacar que cuando se utilizan paths relativos, estos se concatenan, por lo que si tenemos dos controladores con el mismo path, se producirá un error al iniciar la aplicación.

## Versioning

La versión de la API se indica mediante el path de la ruta. En el siguiente ejemplo, la versión de la API es `v1` y el path del controlador es `/users`.

```java
@RestController
@RequiredArgsConstructor
@RequestMapping("/api/v1/users")
public class UserController {
    
    private final UserService userService;
    
    // ...
}
```

Las versiones de la API deben ser compatibles entre sí, por lo que no se deben eliminar o modificar los endpoints de una versión anterior. Si se quiere modificar un endpoint, se debe crear un nuevo endpoint con una nueva versión.

Los paths sin /api/v1 son reservados para endpoints internos de la aplicación, como por ejemplo los endpoints de health check de Spring Actuator.

## @ResponseStatus

La anotación `@ResponseStatus` se utiliza para indicar el código de respuesta HTTP que se devolverá en caso de que no se produzca ninguna excepción. En el siguiente ejemplo, el método `findAll` devuelve un código de respuesta 200 OK.

```java
@RestController
@RequiredArgsConstructor
@RequestMapping("/users")
public class UserController {
    
    private final UserService userService;
    
    @GetMapping
    @ResponseStatus(HttpStatus.OK)
    public List<User> findAll() {
        return userService.findAll();
    }
    
    // ...
}
```

### @PathVariable

La anotación `@PathVariable` se utiliza para mapear una variable de la ruta a un parámetro del método. En el siguiente ejemplo, el parámetro `id` del método `findById` se mapea con la variable `{id}` de la ruta `/users/{id}`.

```java
@RestController
@RequiredArgsConstructor
@RequestMapping("/users")
public class UserController {
    
    private final UserService userService;
    
    @GetMapping("/{id}")
    @ResponseStatus(HttpStatus.OK)
    public User findById(@PathVariable Long id) {
        return userService.findById(id);
    }
    
    @PostMapping
    @ResponseStatus(HttpStatus.CREATED)
    public User create(@RequestBody UserDTO userDTO) {
        return userService.create(userDTO);
    }
    
    // ...
}
```

## Input Data Validation

La validación de los datos de entrada se realiza mediante anotaciones de validación de Bean Validation. Para ello, debemos anotar los parámetros de entrada con las anotaciones de validación correspondientes. La validación se realiza automáticamente antes de ejecutar el método del controlador y si se produce un error, se devuelve un error 400 Bad Request.

Para más información sobre Bean Validation, puedes consultar la [documentación oficial](https://beanvalidation.org/2.0/spec/).

```java
@RestController
@RequiredArgsConstructor
@RequestMapping("/users")
public class UserController {
    
    private final UserService userService;
    
    @PostMapping
    public User create(@Valid @RequestBody User user) {
        return userService.create(user);
    }
    
    // ...
}

public class User {
    
    @NotNull
    private Long id;
    
    @NotBlank
    private String name;
    
    @NotBlank
    private String email;
    
    // ...
}
```

## Pagination

La paginación de los resultados se realiza mediante los parámetros `page` y `size` de la petición HTTP. Estos parámetros se pueden utilizar directamente en el método del controlador, pero nosotros recomendamos utilizar un objeto `Pageable` para recibir estos parámetros y delegar la paginación en el servicio.

```java
@RestController
@RequiredArgsConstructor
@RequestMapping("/users")
public class UserController {
    
    private final UserService userService;
    
    @GetMapping
    public Page<User> findAll(Pageable pageable) {
        return userService.findAll(pageable);
    }
    
    // ...
}
```

