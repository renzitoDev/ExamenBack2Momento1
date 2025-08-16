Repo: https://github.com/renzitoDev/ExamenBack2Momento1.git
***

# Proyecto Examen1Back2 - Gestión Académica Spring Boot

## Descripción del proyecto
Este proyecto es una aplicación backend desarrollada con Java y Spring Boot que gestiona usuarios, docentes y cursos académicos. Utiliza JPA/Hibernate para la persistencia en base de datos y ofrece una arquitectura clara con relaciones uno a uno y uno a muchos entre entidades.

***

## Errores corregidos y explicación

- **Error de anotación JPA en Usuario y Docente**  
  Se corrigió el uso incorrecto de `@OneToMany` sobre campos que no son colecciones; se reemplazó por `@OneToOne` para la relación Usuario-Docente.  
  _Motivo:_ Hibernate exige que `@OneToMany` se use solo con colecciones (List, Set).

- **Error en la relación Docente-Curso**  
  Se cambió `@OneToOne` a `@OneToMany` en la lista de cursos dentro de Docente, para representar correctamente que un docente puede tener muchos cursos.

- **Problema con la referencia del campo en el JoinColumn**  
  Se verificaron los nombres de columnas y claves foráneas para que coincidan correctamente con las tablas y evitar errores de mapeo.

***

## Guía paso a paso para la conexión a la base de datos con Spring Boot

1. **Agregar dependencia JPA y driver en `pom.xml`** (ejemplo para MySQL):

```xml

  org.springframework.boot
  spring-boot-starter-data-jpa


  mysql
  mysql-connector-java
  runtime

```

2. **Configurar `application.properties`** con los datos de conexión:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/tu_base_datos
spring.datasource.username=tu_usuario
spring.datasource.password=tu_contraseña
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
```

3. **Crear entidades JPA anotadas con `@Entity` y relacionarlas correctamente** (como las clases Usuario, Docente, Curso).

4. **Construir la aplicación con Maven**:
```bash
mvn clean package
```

5. **Ejecutar la aplicación**:
```bash
mvn spring-boot:run
```

***

## Recomendaciones para evitar errores similares

- Siempre verifica la **coherencia** entre el tipo de campo y su anotación JPA:
    - `@OneToMany` y `@ManyToMany` deben usarse solo con **colecciones** (`List`, `Set`, etc.).
    - `@OneToOne` y `@ManyToOne` se usan con campos simples (objetos, no colecciones).

- Utiliza siempre el parámetro `mappedBy` para indicar el lado inverso de la relación y evita duplicidades.

- Confirma que los nombres de columnas en `@JoinColumn` coincidan con las columnas de la DB.

- Habilita logging SQL (`spring.jpa.show-sql=true`) para depurar consultas y errores.

- Usa `@JsonManagedReference` y `@JsonBackReference` para evitar **referencias cíclicas** al serializar JSON.

- En casos de eliminaciones en cascada, usa `cascade = CascadeType.REMOVE` para manejar las dependencias de borrado.

***


***

Si quieres que te ayude a generar un archivo `README.md` en formato markdown listo para GitHub o algo más detallado, ¡dímelo!

[1] https://www.codecademy.com/learn/learn-github-best-practices/modules/best-practices-for-teams-on-github/cheatsheet
[2] https://docs.github.com/en/repositories/creating-and-managing-repositories/best-practices-for-repositories
[3] https://dev.to/pwd9000/github-repository-best-practices-23ck
[4] https://www.reddit.com/r/learnprogramming/comments/8u8rrv/what_should_a_github_repo_include_what_is_the/
[5] https://joost.blog/healthy-github-repository/
[6] https://docs.github.com/en/apps/github-marketplace/listing-an-app-on-github-marketplace/writing-a-listing-description-for-your-app
[7] https://www.w3.org/guide/github/best-practices.html
[8] https://docs.github.com/en/contributing/writing-for-github-docs/best-practices-for-github-docs
[9] https://cloud.gov/pages/knowledge-base/repository-best-practices/