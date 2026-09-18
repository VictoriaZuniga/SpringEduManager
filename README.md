# SpringEduManager

Aplicación web educativa desarrollada para la evaluación del Módulo 6: Desarrollo de aplicaciones JEE con Spring Framework. Centraliza estudiantes, cursos, prácticas y evaluaciones mediante una arquitectura MVC, persistencia JPA, seguridad por roles y una API REST.

## Funcionalidades

- Login y logout con Spring Security.
- Roles `ADMIN` y `USER`.
- Panel con resumen de cursos, estudiantes, prácticas y evaluaciones.
- Formularios y listado de estudiantes.
- CRUD web de cursos restringido al rol `ADMIN`.
- Persistencia en H2 mediante Spring Data JPA.
- API REST CRUD para estudiantes y cursos.
- Validación de datos de formularios y JSON.
- Datos iniciales para demostrar el funcionamiento.

## Tecnologías

- Java 17
- Spring Boot 4.1.1
- Spring MVC y Thymeleaf
- Spring Data JPA
- Spring Security
- H2 Database
- Maven Wrapper

## Estructura

```text
src/main/java/cl/bootcamp/springedumanager
├── config       # Seguridad y datos iniciales
├── controller   # Controladores MVC y REST
├── model        # Entidades JPA
├── repository   # Repositorios JpaRepository
└── service      # Lógica de negocio

src/main/resources
├── static/css   # Estilos
├── templates    # Vistas Thymeleaf
└── application.properties
```

## Ejecución

Requisitos: JDK 17 o superior y conexión a Internet en el primer inicio para descargar las dependencias.

### Windows

```powershell
.\mvnw.cmd clean package
.\mvnw.cmd spring-boot:run
```

### Linux o macOS

```bash
./mvnw clean package
./mvnw spring-boot:run
```

Abrir `http://localhost:8080`.

## Usuarios de demostración

| Rol | Usuario | Contraseña | Permisos |
|---|---|---|---|
| ADMIN | `admin` | `Admin123!` | Consulta y administración de cursos |
| USER | `estudiante` | `User123!` | Consulta y gestión de estudiantes |

Estas credenciales son únicamente para evaluación local. En producción deben reemplazarse por usuarios almacenados de forma segura y secretos externos.

## Base de datos H2

- Consola: `http://localhost:8080/h2-console`
- JDBC URL: `jdbc:h2:file:./data/springedumanager`
- Usuario: `sa`
- Contraseña: vacía

La consola está disponible solo para el usuario administrador.

## API REST

La API utiliza autenticación HTTP Basic. Los ejemplos siguientes usan el usuario administrador.

```bash
# Listar cursos
curl -u admin:Admin123! http://localhost:8080/api/cursos

# Crear curso (solo ADMIN)
curl -u admin:Admin123! -H "Content-Type: application/json" \
  -d '{"nombre":"APIs con Spring","descripcion":"Diseño de servicios REST","duracionHoras":24}' \
  http://localhost:8080/api/cursos

# Actualizar curso
curl -u admin:Admin123! -X PUT -H "Content-Type: application/json" \
  -d '{"nombre":"APIs REST con Spring","descripcion":"CRUD e interoperabilidad","duracionHoras":30}' \
  http://localhost:8080/api/cursos/1

# Eliminar curso
curl -u admin:Admin123! -X DELETE http://localhost:8080/api/cursos/3

# Listar estudiantes
curl -u estudiante:User123! http://localhost:8080/api/estudiantes
```

También se incluye la colección `postman/SpringEduManager.postman_collection.json`.

## Comandos Maven solicitados

```bash
./mvnw clean
./mvnw install
./mvnw package
```

El ejecutable se genera en `target/springedumanager-0.0.1-SNAPSHOT.jar`.

## Evidencias y trazabilidad

- Revisar `docs/INFORME_ENTREGA.md` para la relación entre la pauta y la implementación.
- El repositorio completo constituye la evidencia técnica y puede publicarse directamente en GitHub.
- La colección Postman permite demostrar las operaciones REST durante la evaluación.
- La prueba `SpringEduManagerApplicationTests` verifica que el contexto de Spring se cargue correctamente.

## Referencias técnicas

- [Spring Boot Reference Documentation](https://docs.spring.io/spring-boot/index.html)
- [Spring Security Reference](https://docs.spring.io/spring-security/reference/)
- [Spring Data JPA Reference](https://docs.spring.io/spring-data/jpa/reference/)
- [Thymeleaf + Spring](https://www.thymeleaf.org/doc/tutorials/3.1/thymeleafspring.html)
- [Apache Maven](https://maven.apache.org/guides/)
