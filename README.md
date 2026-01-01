# LSI-MAX: Aplicación de Streaming

<p align="center">
  <!-- Java -->
  <img src="https://img.shields.io/badge/Java-11-007396?logo=openjdk&logoColor=white" alt="Java 11"/>
  <!-- Spring Boot -->
  <img src="https://img.shields.io/badge/Spring%20Boot-2.7.x-6DB33F?logo=springboot&logoColor=white" alt="Spring Boot"/>
  <!-- Spring Security -->
  <img src="https://img.shields.io/badge/Spring%20Security-5.x-6DB33F?logo=springsecurity&logoColor=white" alt="Spring Security"/>
  <!-- H2 Database -->
  <img src="https://img.shields.io/badge/H2-Database-004088?logo=h2&logoColor=white" alt="H2 Database"/>
  <!-- JPA -->
  <img src="https://img.shields.io/badge/Spring%20Data%20JPA-Enabled-blue" alt="Spring Data JPA"/>
  <!-- MapStruct -->
  <img src="https://img.shields.io/badge/MapStruct-1.5.5.Final-ff4081" alt="MapStruct"/>
  <!-- Thymeleaf -->
  <img src="https://img.shields.io/badge/Thymeleaf-Enabled-005f0f?logo=thymeleaf&logoColor=white" alt="Thymeleaf"/>
  <!-- Maven -->
  <img src="https://img.shields.io/badge/Maven-Build-CA4245?logo=apachemaven&logoColor=white" alt="Maven"/>
  <!-- Arquitectura -->
  <img src="https://img.shields.io/badge/Arquitectura-Hexagonal-blueviolet" alt="Arquitectura Hexagonal"/>
  <!-- Licencia -->
  <img src="https://img.shields.io/badge/Licencia-MIT-yellow" alt="MIT License"/>
</p>

<p align="center">
  <img src="/screenshots/home.png" alt="Página principal" width="500"/>
</p>

## Resumen del Proyecto

**LSI-MAX** es una aplicación Fullstack que simula un servicio de Streaming de Video por Suscripción (SVOD). Permite gestionar:

* Catálogo de contenidos multimedia.
* Suscripciones y roles de usuario.
* Acceso seguro a contenido según permisos.

El proyecto está diseñado con Arquitectura Hexagonal (Puertos y Adaptadores) para garantizar una separación estricta de responsabilidades y alta testabilidad. Esto permite que el Core del Dominio permanezca completamente independiente de detalles de infraestructura como bases de datos, interfaces de usuario o APIs externas.

---

## Tecnologías

| Categoría        | Tecnología                   | Versión     | Propósito / Habilidad demostrada                                   |
| :--------------- | :--------------------------- | :---------- | :----------------------------------------------------------------- |
| **Lenguaje**     | Java                         | 11 (LTS)    | Estándar en aplicaciones empresariales.                            |
| **Framework**    | Spring Boot                  | 2.7.x       | Construcción de servicios robustos y modulares.                    |
| **Arquitectura** | Hexagonal (Ports & Adapters) | N/A         | Modularidad, bajo acoplamiento, **preparada para microservicios**. |
| **Seguridad**    | Spring Security              | 5.x         | Autenticación basada en roles y protección de endpoints.           |
| **Persistencia** | Spring Data JPA / H2         | N/A         | Gestión relacional de datos; H2 para desarrollo y pruebas.         |
| **Mapeo**        | MapStruct                    | 1.5.5.Final | Transformación eficiente de DTOs a Entities.                       |
| **Frontend**     | Thymeleaf                    | N/A         | Presentación dinámica integrada con Spring Security.               |
| **Build Tool**   | Maven                        | N/A         | Gestión de dependencias y ciclo de vida de la aplicación.          |

---

## Arquitectura Hexagonal en LSI-MAX

El proyecto sigue fielmente el patrón **Ports & Adapters**, aislando el núcleo de negocio. Los principales paquetes son:

1. **`domain`**
   Contiene las reglas de negocio y casos de uso (CRUD). **No tiene dependencias de infraestructura.**

2. **`application`**
   Define los **Ports** (interfaces) y contiene los **Primary Adapters** (servicios que coordinan los casos de uso).

   * **`port`**: Interfaces de servicios (Primary Ports) y repositorios (Secondary Ports).
   * **`service`**: Implementa casos de uso coordinando Domain y Secondary Ports.

3. **`infrastructure`**
   Implementa los **Adapters** que cumplen los contratos definidos por los Ports.

   * **`adapter.inbound`**: Entrada de datos desde controladores REST y vistas Thymeleaf.
   * **`adapter.outbound`**: Salida hacia bases de datos usando Spring Data JPA.

<!--p align="center">
  <img src="/screenshots/contentDetail.png" alt="Detalle de contenido" width="500"/>
</p-->

---

## Funcionalidades Clave

* Gestión de catálogo de contenidos (CRUD completo).
* Suscripciones y roles de usuario (ADMIN, EMPLOYEE, MEMBER).
* Dashboard de administración con analíticas y estadísticas de uso.
* Autenticación y autorización basadas en roles con Spring Security.
* Interfaz dinámica con Thymeleaf.

---

## Ejecución Local

1. **Clonar repositorio:**

```bash
git clone https://github.com/Jherna77/streaming-spring-hexagonal.git
cd streaming-spring-hexagonal
```

2. **Compilar y empaquetar:**

```bash
mvn clean install
```

3. **Ejecutar la aplicación:**

```bash
java -jar target/lsi-max-1.0.jar
```

Accede a la aplicación en `http://localhost:8080`.

---

## Credenciales de Acceso

| Rol           | Email                                           | Contraseña |
| :------------ | :---------------------------------------------- | :--------- |
| Administrador | [admin@lsimax.es](mailto:admin@lsimax.es)       | password   |
| Empleado      | [employee@lsimax.es](mailto:employee@lsimax.es) | password   |
| Miembro       | [member@lsimax.es](mailto:member@lsimax.es)     | password   |

<p align="center">
  <img src="/screenshots/login.png" alt="Pantalla de login" width="500"/>
</p>

### Dashboard de Administrador

Solo accesible con rol **ADMIN**. Permite:

* Monitoreo de métricas clave (valoración de contenido, reproducciones).
* Análisis de consumo y tendencias de usuarios.
* Gestión del catálogo de contenido y roles.

<p align="center">
  <img src="/screenshots/adminDashboard.png" alt="Dashboard de administrador" width="500"/>
</p>

---

## Pruebas

Gracias a la Arquitectura Hexagonal, el núcleo es altamente testeable.

* **Herramientas:** JUnit 5 y Spring Security Test.
* **Ejecutar pruebas:**

```bash
mvn test
```
