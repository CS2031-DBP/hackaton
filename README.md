# Sistema de Reserva de Salones 📅✨

## Calificación 

La evaluación se realizará mostrando el funcionamiento de los endpoints en vivo a uno de los miembros del jurado. Deberán crear sus endpoints en Postman para testear la funcionalidad. Solo si se demuestra la funcionalidad completa de todo el sistema se otorgará el puntaje completo.

## Descripción del Caso

El objetivo de este proyecto es desarrollar un sistema de reservas que permita a los usuarios registrarse, iniciar sesión y realizar reservas en diferentes salones disponibles. Este sistema gestionará las siguientes entidades:

- *Usuario* 🧑‍💻
- *Salón* 🏢
- *Reserva* 📅
- *Etiqueta* 🏷

Además, se incluirá la funcionalidad de autenticación (registro e inicio de sesión) y una entidad adicional para manejar una relación de muchos a muchos.

## Requisitos del Sistema

1. *Autenticación y Gestión de Usuarios:*
   - Registro de usuarios.
   - Inicio de sesión de usuarios.

2. *Gestión de Salones:*
   - Información sobre los salones disponibles para reservas.

3. *Gestión de Reservas:*
   - Permitir a los usuarios realizar reservas en los salones para rangos de tiempo específicos.

4. *Relación Muchos a Muchos:*
   - Implementación de una entidad adicional para manejar una relación de muchos a muchos.

## Diagrama de Clases con Mermaid 📚

mermaid
classDiagram
    class Usuario {
        +int idUsuario
        +String nombre
        +String correoElectronico
        +String contraseña
        +String telefono
    }

    class Salon {
        +int idSalon
        +String nombre
        +String ubicacion
        +int capacidad
        +String descripcion
    }

    class Reserva {
        +int idReserva
        +Date fecha
        +Time horaInicio
        +Time horaFin
    }

    class Etiqueta {
        +int idEtiqueta
        +String nombre
    }

    class SalonEtiqueta {
        +int idSalon
        +int idEtiqueta
    }

    Usuario "1" --> "0..*" Reserva : hace
    Salon "1" --> "0..*" Reserva : tiene
    Salon "1" --> "0..*" SalonEtiqueta : pertenece
    Etiqueta "1" --> "0..*" SalonEtiqueta : categoriza
    Reserva "*" --> "1" Usuario : pertenece
    Reserva "*" --> "1" Salon : pertenece


## Funcionalidades 🌟

1. *Autenticación:*
   - *Registro*: Endpoint para que los usuarios se registren proporcionando nombre, correo electrónico, contraseña y teléfono.
   - *Inicio de sesión*: Endpoint para que los usuarios se autentiquen utilizando su correo electrónico y contraseña.

2. *Gestión de Salones:*
   - *CRUD*: Endpoints para crear, leer, actualizar y eliminar información de los salones.

3. *Gestión de Reservas:*
   - *Realizar Reserva*: Endpoint para que los usuarios reserven un salón especificando fecha y hora.

4. *Relación Muchos a Muchos:*
   - *Etiquetado de Salones*: Endpoints para asociar etiquetas a los salones y viceversa.

No se puede hacer una reserva si ese horario ya está ocupado.

## Endpoints 🚀

- *Registro de Usuario:*
  - POST /usuarios/register
- *Inicio de Sesión:*
  - POST /usuarios/login
- *Gestión de Salones:*
  - GET /salones
  - POST /salones
  - PUT /salones/{id}
  - DELETE /salones/{id}
- *Gestión de Reservas:*
  - GET /reservas
  - POST /reservas
  - PUT /reservas/{id}
  - DELETE /reservas/{id}
- *Gestión de Etiquetas:*
  - GET /etiquetas
  - POST /etiquetas
  - PUT /etiquetas/{id}
  - DELETE /etiquetas/{id}
- *Asociación de Salones y Etiquetas:*
  - POST /salones/{idSalon}/etiquetas/{idEtiqueta}
  - DELETE /salones/{idSalon}/etiquetas/{idEtiqueta}

## Eventos y Asincronía 🎉

Cada vez que un usuario realiza una reserva, se enviará un correo electrónico de confirmación al usuario. Para ello, se implementará un servicio de envío de correos electrónicos que se ejecute de forma asíncrona. Este servicio se encargará de enviar el correo electrónico de confirmación al usuario.

Para lograr esto, se implementará un sistema de eventos que se dispare cada vez que se realice una reserva de manera asíncrona.
