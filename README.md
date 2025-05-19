#📚 Documentación del Sistema de Gestión de Biblioteca Digital
#🧩 Arquitectura General
El sistema está basado en una arquitectura de microservicios implementada con Spring Boot, donde cada funcionalidad principal se encuentra desacoplada en su propio servicio. Esto permite mayor mantenibilidad, escalabilidad y facilidad de despliegue.
#⚙️ Tecnologías Utilizadas
Java 17+

Spring Boot

Web

Data JPA

Lombok

MySQL (una base por servicio)

H2 (alternativa para pruebas locales)

Postman (para pruebas)

Maven (gestión de dependencias)
    
                                  ┌────────────────────────────┐
                                  │ Cliente (Postman / Frontend)│
                                  └────────────▲────────────────┘
                                               │
                                    REST APIs (HTTP JSON)
                                               │
            ┌────────────────────┬────────────┬─────────────┬────────────────┬───────────────┬────────────────┐
        ┌───▼─────────────┐ ┌─────▼─────────┐ ┌─▼─────────────┐ ┌────────────▼───┐ ┌──────────▼─────┐ ┌────────▼────────────┐
        │ Servicio        │ │ Servicio      │ │ Servicio      │ │ Servicio       │ │ Servicio       │ │ Servicio            │
        │ Usuarios        │ │ Cursos        │ │ Inscripciones │ │ Pagos          │ │ Soporte        │ │ Evaluaciones        │
        │ /api/v1/usuarios│ │ /api/v1/cursos│ │ /api/v1/insc  │ │ /api/v1/pagos  │ │ /api/v1/soporte│ │ /api/v1/evaluaciones│
        └────┬────────────┘ └────┬──────────┘ └────┬──────────┘ └───────┬────────┘ └───────┬────────┘ └───────┬─────────────┘
             ▼                   ▼                 ▼                    ▼                  ▼                 ▼
         🗃️ db_usuarios    🗃️ db_cursos      🗃️ db_inscripciones   🗃️ db_pagos      🗃️ db_soporte     🗃️ db_evaluaciones

#🗂️ Microservicios
1. Servicio de Cursos
Propósito: Gestiona los cursos disponibles en la biblioteca digital.
Puerto: 8081
Base de datos: db_cursos
Endpoints:
GET /api/v1/cursos
POST /api/v1/cursos
PUT /api/v1/cursos/{id}
DELETE /api/v1/cursos/{id}

2. Servicio de Usuarios
Propósito: Gestiona la información de los usuarios (nombre, correo, rol, etc.)
Puerto: 8082
Base de datos: db_usuarios
Endpoints:
GET /api/v1/usuarios
POST /api/v1/usuarios
PUT /api/v1/usuarios/{id}
DELETE /api/v1/usuarios/{id}

3. Servicio de Inscripciones
Propósito: Permite inscribir usuarios en cursos.
Puerto: 8083
Base de datos: db_inscripcion
Campos clave: idUsuario, idCurso
Endpoints:
GET /api/v1/inscripciones
POST /api/v1/inscripciones
DELETE /api/v1/inscripciones/{id}

4. Servicio de Pagos
Propósito: Registra y consulta pagos de los usuarios.
Puerto: 8084
Base de datos: db_pagos
Endpoints:
GET /api/v1/pagos
POST /api/v1/pagos
DELETE /api/v1/pagos/{id}

5. Servicio de Soporte
Propósito: Permite que los usuarios envíen solicitudes o problemas técnicos.
Puerto: 8085
Base de datos: db_soporte
Endpoints:
GET /api/v1/soporte
POST /api/v1/soporte
DELETE /api/v1/soporte/{id}

6. Servicio de Evaluación
Propósito: Registra calificaciones de usuarios en cursos.
Puerto: 8086
Base de datos: db_evaluacion
Endpoints:
GET /api/v1/evaluaciones
POST /api/v1/evaluaciones
PUT /api/v1/evaluaciones/{id}
DELETE /api/v1/evaluaciones/{id}

7. Servicio de Reportes
Propósito: Genera y almacena reportes (manuales o automáticos).
Puerto: 8087
Base de datos: db_reportes
Endpoints:
GET /api/v1/reportes
POST /api/v1/reportes
DELETE /api/v1/reportes/{id}

#🧱 Estructura del código por microservicio
Cada microservicio sigue la siguiente convención de estructura de carpetas:

    src/
    ├── controller/       → Exposición de endpoints REST
    ├── service/          → Lógica de negocio
    ├── repository/       → Acceso a datos vía JPA
    ├── model/            → Entidades JPA
    └── application.properties → Configuración por servicio
