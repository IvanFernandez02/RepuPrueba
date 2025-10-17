# AthletIA - Mini Dossier

**Integrantes:**
* Gabriel Cevallos
* David Paccha
* Ivan Fernandez

**Repositorio:** [https://github.com/GabrielCevallos/AthletIA](https://github.com/GabrielCevallos/AthletIA)

---

## Introducción

AthletIA es una API RESTful diseñada para la gestión integral de usuarios y rutinas de entrenamiento. Su propósito es ofrecer un conjunto completo de operaciones **CRUD (Crear, Leer, Actualizar, Eliminar)** para facilitar la integración de funcionalidades de fitness en cualquier tipo de aplicación de software.

La API está estructurada en módulos, cada uno con responsabilidades específicas, desde la autenticación y gestión de cuentas hasta la administración de perfiles y ejercicios.

---

## Endpoints Desarrollados

A continuación se detallan los endpoints implementados, agrupados por funcionalidad.

### 🔑 AUTH

Este módulo gestiona la autenticación, registro y seguridad de las cuentas.

| Ruta | Método | Descripción | Parámetros | Códigos de Respuesta |
| :--- | :--- | :--- | :--- | :--- |
| `/auth/login` | `POST` | Autentica credenciales y emite un token JWT. | **Body:** `email` (string), `password` (string) | `200`, `400`, `401`, `500` |
| `/auth/register-account` | `POST` | Registra una nueva cuenta de usuario. | **Body:** `email` (string), `password` (string) | `201`, `400`, `500` |
| `/auth/complete-profile-setup` | `POST` | Completa la configuración del perfil del usuario tras el registro. | **Body:** `accountId` (string), `profileRequest` (object) | `201`, `400`, `500` |
| `/auth/change-password` | `PATCH` | Permite a un usuario autenticado cambiar su contraseña. | **Body:** `accountId`, `oldPassword`, `newPassword` | `200`, `400`, `401`, `404`, `500` |
| `/auth/refresh-token` | `POST` | Genera un nuevo token de acceso usando un token de refresco. | **Body:** `refreshToken` (string) | `200`, `400`, `500` |
| `/auth/logout` | `POST` | Cierra la sesión del usuario invalidando su token de refresco. | **Body:** `accountId` (string) | `200`, `401`, `500` |

---

### 👤 ACCOUNT

Endpoints dedicados a la administración de cuentas de usuario. Requieren roles específicos.

| Ruta | Método | Descripción | Parámetros | Códigos de Respuesta |
| :--- | :--- | :--- | :--- | :--- |
| `/users` | `GET` | Obtiene una lista paginada de usuarios. **Rol requerido: ADMIN o MODERATOR**. | **Query:** `page`, `limit`, `search` | `200`, `403`, `500` |
| `/users/:id` | `GET` | Obtiene la información detallada de un usuario. **Rol requerido: ADMIN o MODERATOR**. | **URL:** `id` del usuario | `200`, `401`, `403`, `404`, `500` |
| `/users/:id/suspend` | `PATCH` | Suspende la cuenta de un usuario. **Rol requerido: ADMIN o MODERATOR**. | **URL:** `id` del usuario | `200`, `401`, `403`, `404`, `500` |
| `/users/:id/give-role` | `PATCH` | Asigna o cambia el rol de un usuario. **Rol requerido: ADMIN**. | **URL:** `id` del usuario, **Body:** `role` | `200`, `400`, `401`, `403`, `404`, `500` |

---

### 📄 PROFILES

Módulo para la gestión de los perfiles públicos y privados de los usuarios.

| Ruta | Método | Descripción | Parámetros | Códigos de Respuesta |
| :--- | :--- | :--- | :--- | :--- |
| `/profiles/:id` | `GET` | Obtiene la información detallada de un perfil. **Requiere autenticación**. | **URL:** `id` del perfil | `200`, `401`, `404`, `500` |
| `/profiles/:id` | `PATCH` | Actualiza la información de un perfil. Un usuario solo puede actualizar su propio perfil (a menos que sea ADMIN). | **URL:** `id` del perfil, **Body:** campos a actualizar | `200`, `400`, `401`, `403`, `404`, `500` |

---

### 💪 EXERCISES

Endpoints para la gestión de los ejercicios de entrenamiento.

| Ruta | Método | Descripción | Parámetros | Códigos de Respuesta |
| :--- | :--- | :--- | :--- | :--- |
| `/workout/exercises` | `POST` | Crea un nuevo ejercicio. | **Body:** datos del ejercicio | `201`, `400`, `500` |
| `/workout/exercises` | `GET` | Obtiene una lista de todos los ejercicios. | Ninguno | `200`, `500` |
| `/workout/exercises/:id` | `GET` | Obtiene la información detallada de un ejercicio. | **URL:** `id` del ejercicio | `200`, `404`, `500` |
| `/workout/exercises/:id` | `PATCH` | Actualiza parcialmente un ejercicio existente. | **URL:** `id` del ejercicio, **Body:** campos a actualizar | `200`, `400`, `404`, `500` |
| `/workout/exercises/:id` | `DELETE` | Elimina un ejercicio de forma permanente. | **URL:** `id` del ejercicio | `204`, `404`, `500` |

---

## Pruebas Realizadas en Postman

Para garantizar el correcto funcionamiento de la API, se realizaron pruebas exhaustivas en cada uno de los endpoints utilizando **Postman**. Las pruebas cubrieron:

- **Peticiones exitosas (Happy Paths):** Verificación de respuestas con código `200` y `201`, asegurando que los datos se creen, lean, actualicen y eliminen correctamente.
- **Errores de cliente:** Comprobación de respuestas `400` (Bad Request), `401` (Unauthorized), `403` (Forbidden) y `404` (Not Found) al enviar datos incorrectos o sin los permisos adecuados.
- **Validación de datos:** Pruebas para asegurar que los datos de entrada son validados correctamente antes de ser procesados.

A continuación, se muestran algunas capturas de pantalla de las pruebas ejecutadas:

<img width="486" height="274" alt="image" src="https://github.com/user-attachments/assets/16596bc9-662a-4a45-951c-b638d61aec2b" />  <img width="486" height="274" alt="image" src="https://github.com/user-attachments/assets/5a67c3b3-04ae-4f21-9b6f-c0ded3c09624" />

<img width="487" height="274" alt="image" src="https://github.com/user-attachments/assets/93f8a6d8-2a48-4867-b647-ec94bc019161" />  <img width="486" height="274" alt="image" src="https://github.com/user-attachments/assets/14da3f38-0ff3-48a5-8bb8-a70508c88754" />

<img width="487" height="274" alt="image" src="https://github.com/user-attachments/assets/bc81f264-2dde-4ba7-86a5-dd55cdd88b84" />  <img width="486" height="274" alt="image" src="https://github.com/user-attachments/assets/8b8e1aca-58bc-4677-a131-cfe337d295df" />

<img width="487" height="274" alt="image" src="https://github.com/user-attachments/assets/22a3441d-0a1b-4c26-951f-0079ca373576" />  <img width="486" height="274" alt="image" src="https://github.com/user-attachments/assets/41175fd3-db0a-4832-be38-8a66814b8fbe" />

<img width="480" height="270" alt="image" src="https://github.com/user-attachments/assets/dab61523-222b-40d9-ac4a-61d71b937bf2" />  <img width="486" height="274" alt="image" src="https://github.com/user-attachments/assets/a537840f-2072-4d05-a33e-8e0d50b65b18" />

<img width="487" height="274" alt="image" src="https://github.com/user-attachments/assets/b713ae10-b56f-4e1e-919c-6f364d3849fc" />  <img width="486" height="274" alt="image" src="https://github.com/user-attachments/assets/d0b8c213-9a49-4b2d-b866-8bb137428db5" />

<img width="487" height="274" alt="image" src="https://github.com/user-attachments/assets/f5f89b80-f39f-4bb2-bf5e-10b9b22ae3ad" />  <img width="486" height="274" alt="image" src="https://github.com/user-attachments/assets/f26b8e69-37b4-417a-bd28-9b342912c012" />

<img width="487" height="274" alt="image" src="https://github.com/user-attachments/assets/5e1431ff-d67c-474f-a474-9329696f9d70" />
