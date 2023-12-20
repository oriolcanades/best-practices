# Best Practices for Spring Boot Applications

## Table of Contents

<!-- TOC -->
* [Best Practices for Spring Boot Applications](#best-practices-for-spring-boot-applications)
  * [Table of Contents](#table-of-contents)
  * [Estructuras del proyecto y configuraciones](#estructuras-del-proyecto-y-configuraciones)
  * [Estándares de codificación](#estándares-de-codificación)
  * [Diseño y Arquitectura](#diseño-y-arquitectura)
  * [Testing](#testing)
  * [Seguridad](#seguridad)
  * [Documentación](#documentación)
  * [Despliegue y Operaciones](#despliegue-y-operaciones)
  * [Consideraciones Generales](#consideraciones-generales)
  * [References](#references)
<!-- TOC -->

## Estructuras del proyecto y configuraciones

- [ ] Estructura de un proyecto Spring Boot
    - [ ] Maven vs. Gradle
    - [ ] Control de versiones
    - [ ] Gestión de dependencias
    - [ ] Estructura de directorios
- [ ] Configuraciones básicas
    - [ ] Validation
    - [ ] Actuator
    - [ ] Lombok
    - [ ] MapStruct
    - [ ] Swagger
    - [ ] Jacoco
- [ ] Configuraciones de entorno
    - [ ] Spring Profiles
    - [ ] Spring Cloud Config
    - [ ] Consul

## Estándares de codificación

- [ ] Guías de estilo
    - [ ] Checkstyle + Google Java Style Guide
- [ ] Naming convention
    - [ ] Resource Naming Conventions
    - [ ] Http Status Codes
- [ ] Comentarios y documentación de código
    - [ ] JavaDoc
    - [ ] Clases y métodos
- [ ] Principios SOLID
- [ ] Pruebas de Linting
    - [ ] Sonar
    - [ ] Checkstyle
    - [ ] FindBugs / SpotBugs / Find Security Bugs
- [ ] Refactoring

## Diseño y Arquitectura

- [ ] Patrones de diseño
    - [ ] Resiliencia & Circuit Breaker
        - [ ] Spring Retry
        - [ ] Resilience4j
- [ ] API Restful Design
    - [ ] [Controllers](diseño-y-arquitectura/api-restful-design/controllers.md)
        - [ ] [Input Data Validation](diseño-y-arquitectura/api-restful-design/controllers.md#input-data-validation)
        - [ ] [Pagination](diseño-y-arquitectura/api-restful-design/controllers.md#pagination)
        - [ ] [Versioning](diseño-y-arquitectura/api-restful-design/controllers.md#versioning)
    - [ ] Services
        - [x] [Builder](diseño-y-arquitectura/patrones-de-diseño/builder-pattern.md)
        - [x] [DTO](diseño-y-arquitectura/patrones-de-diseño/dto-pattern.md)
        - [ ] Facade
    - [ ] Repositories
        - [ ] Spring Data JPA
        - [ ] Spring Data JDBC
        - [ ] Spring Data R2DBC
    - [ ] [Error Handling](diseño-y-arquitectura/api-restful-design/error-handling.md)
        - [ ] [Custom Exceptions](diseño-y-arquitectura/api-restful-design/error-handling.md#custom-exceptions)
        - [ ] [Global Exception Handler](diseño-y-arquitectura/api-restful-design/error-handling.md#global-exception-handler)
        - [ ] [Custom Error Response](diseño-y-arquitectura/api-restful-design/error-handling.md#custom-error-response)
- [ ] Layer Architecture
- [ ] Microservices Architecture
- [ ] Event Driven Architecture
- [ ] Caching
    - [ ] Redis
    - [ ] EhCache
- [ ] Database Migrations
    - [ ] Liquibase
    - [ ] Flyway
- [ ] API Gateway

## Testing

- [ ] Pruebas unitarias
    - [ ] JUnit & Mockito
- [ ] Pruebas de integración
    - [ ] Spring Cloud Contract
- [ ] Code Coverage
    - [ ] Jacoco
- [ ] Pruebas de rendimiento
    - [ ] JMeter
    - [ ] Gatling
- [ ] Integración Continua (CI)
    - [ ] GitHub Actions
    - [ ] Azure Pipelines
- [ ] Testing de Seguridad
    - [ ] Pruebas de penetración
    - [ ] Análisis de vulnerabilidades
- [ ] Behavior Driven Development (BDD)
    - [ ] Cucumber

## Seguridad

- [ ] Autenticación y autorización
    - [ ] Spring Security
    - [ ] OAuth2
    - [ ] JWT
- [ ] OWASP Dependency Check
- [ ] Validación de entrada
    - [ ] SQL Injection
    - [ ] XSS
- [ ] Seguridad en aplicación
    - [ ] DoS
- [ ] Cifrado y seguridad de datos.
    - [ ] Bcrypt
    - [ ] AES
    - [ ] RSA
- [ ] HTTPS
- [ ] Snyk / WhiteSource - Vulnerability Scanner
- [ ] Gestión de Secrets
    - [ ] Hashicorp Vault
    - [ ] Azure Key Vault

## Documentación

- [ ] Documentación de API
    - [ ] Swagger
    - [ ] OpenAPI
- [ ] Logs y Monitorización
    - [ ] Actuator
    - [ ] Logback
    - [ ] Micrometer
    - [ ] Prometheus
    - [ ] Grafana
- [ ] Monitorización distribuida
    - [ ] Jaeger
    - [ ] Zipkin
- [ ] Guías de Usuario y Administrador
    - [ ] README.md
    - [ ] CHANGELOG.md

## Despliegue y Operaciones

- [ ] Docker - Contenedores
    - [ ] Dockerfile
- [ ] Kubernetes - Orquestación
- [ ] Helm-Charts
- [ ] CI/CD
    - [ ] GitHub Actions
    - [ ] Azure Pipelines
- [ ] Cloud
    - [ ] Azure
- [ ] Configuración de Logs y Monitoreo en Kubernetes
- [ ] IaaS, PaaS, SaaS Considerations
- [ ] Monitoreo y Alertas
- [ ] Escalabilidad y Alta Disponibilidad

## Consideraciones Generales

- [ ] Casos de Uso y Escenarios Prácticos
- [ ] Evolución y Mantenimiento a Largo Plazo`

## References

- https://www.javaguides.net/2023/11/spring-boot-rest-api-best-practices.html
- 