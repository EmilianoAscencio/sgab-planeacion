# Definición de Requisitos Funcionales traducidos a Endpoints
Sistema de Gestión Académica Básico (SGAB)

---

## 1. Introducción

En este documento se especifica la implementación técnica de los requisitos funcionales del SGAB mediante endpoints REST.

Cada requisito funcional se transforma en:

Requisito Funcional → Método HTTP → Endpoint → Reglas de negocio → Respuesta esperada

---

# 2. Módulo Alumnos (Students)

Base URL: /api/students

---

## RF-01 y RF-02 – Gestión de alumnos

### 2.1 Crear alumno

POST /api/students

Descripción:
Registrar un nuevo alumno en el sistema.

Body:

{
  "matricula": "string",
  "nombre": "string",
  "carrera": "string",
  "correo": "string"
}

Reglas de negocio:
- La matrícula debe ser única.
- Todos los campos son obligatorios.
- El alumno se crea con estado = "active".
- Validar formato de correo.

Respuesta:
- 201 Created
- 400 Bad Request si faltan campos
- 409 Conflict si la matrícula ya existe

---

### 2.2 Listar alumnos

GET /api/students

Query params opcionales:
?status=active
?page=1&limit=10

Respuesta:

{
  "data": [],
  "pagination": {
    "page": 1,
    "limit": 10,
    "total": number
  }
}

---

### 2.3 Obtener alumno por ID

GET /api/students/{id}

Reglas:
- El alumno debe existir.
- Si no existe → 404 Not Found.

---

### 2.4 Actualizar alumno

PUT /api/students/{id}

Body:

{
  "nombre": "string",
  "carrera": "string",
  "correo": "string",
  "status": "active | inactive"
}

Reglas:
- Validar existencia.
- Validar unicidad si cambia matrícula.
- No permitir eliminar matrícula si tiene calificaciones registradas.

Respuesta:
- 200 OK
- 404 Not Found

---

### 2.5 Eliminación lógica

DELETE /api/students/{id}

Regla:
- Cambiar status a "inactive".
- No eliminar físicamente el registro.

Respuesta:
- 204 No Content

---

# 3. Módulo Materias (Subjects)

Base URL: /api/subjects

---

## RF-03 – Gestión de materias

### 3.1 Crear materia

POST /api/subjects

Body:

{
  "clave": "string",
  "nombre": "string",
  "creditos": number
}

Reglas:
- Clave única.
- Créditos > 0.
- Campos obligatorios.

Respuesta:
- 201 Created
- 409 Conflict si clave duplicada

---

### 3.2 Listar materias

GET /api/subjects

Respuesta:
- 200 OK + arreglo de materias

---

### 3.3 Consultar materia

GET /api/subjects/{id}

Respuesta:
- 200 OK
- 404 Not Found

---

### 3.4 Actualizar materia

PATCH /api/subjects/{id}

Reglas:
- Validar existencia.
- No permitir modificar clave si ya está asignada.

---

### 3.5 Eliminación lógica

DELETE /api/subjects/{id}

Regla:
- Marcar como inactiva.
- No borrar si tiene calificaciones asociadas.

---

# 4. Módulo Calificaciones (Grades)

Base URL: /api/grades

---

## RF-05 y RF-06 – Gestión de calificaciones

### 4.1 Registrar calificación

POST /api/grades

Body:

{
  "studentId": "string",
  "subjectId": "string",
  "valor": number
}

Reglas:
- El alumno debe existir y estar activo.
- La materia debe existir.
- Valor entre 0 y 100.
- No duplicar calificación para misma materia y alumno.

Respuesta:
- 201 Created
- 400 Bad Request
- 404 Not Found

---

### 4.2 Listar calificaciones

GET /api/grades

Filtros opcionales:
?studentId=
?subjectId=

---

### 4.3 Obtener calificación

GET /api/grades/{id}

---

### 4.4 Actualizar calificación

PATCH /api/grades/{id}

Reglas:
- Validar rango 0–100.
- Registrar acción en bitácora (RNF-06).

---

### 4.5 Eliminar calificación

DELETE /api/grades/{id}

Regla:
- Eliminación lógica.
- Registrar en auditoría.

---

# 5. Módulo Usuarios y Autenticación

Base URL: /api/users

---

## RF-08 – Autenticación y gestión de usuarios

### 5.1 Crear usuario

POST /api/users

Body:

{
  "nombre": "string",
  "email": "string",
  "password": "string",
  "role": "admin | teacher"
}

Reglas:
- Email único.
- Password mínimo 8 caracteres.
- Encriptar contraseña.
- Asignar rol válido.

Respuesta:
- 201 Created
- 409 Conflict

---

### 5.2 Autenticación

POST /api/auth/login

Body:

{
  "email": "string",
  "password": "string"
}

Respuesta:

{
  "token": "jwt_token",
  "expiresIn": "1h"
}

Reglas:
- Validar credenciales.
- Generar JWT.
- Token requerido para endpoints protegidos.

---

### 5.3 Obtener perfil autenticado

GET /api/auth/me

Header:
Authorization: Bearer {token}

Respuesta:
- 200 OK
- 401 Unauthorized si token inválido