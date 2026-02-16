# Requisitos No Funcionales

## RNF-01 (Rendimiento)
El sistema deberá responder a cualquier consulta en un tiempo menor a 2 segundos bajo carga normal (hasta 50 usuarios concurrentes).

## RNF-02 (Seguridad)
El sistema deberá requerir autenticación obligatoria para acceder a cualquier módulo.

## RNF-03 (Control de acceso)
El sistema deberá implementar control de roles (Administrativo y Docente) restringiendo funciones según perfil.

## RNF-04 (Disponibilidad)
El sistema deberá estar disponible al menos el 99% del tiempo durante horario escolar.

## RNF-05 (Persistencia)
La información deberá almacenarse en una base de datos relacional y mantenerse después de reinicios del sistema.

## RNF-06 (Auditoría)
El sistema deberá registrar en bitácora las acciones críticas (registro, modificación y eliminación de datos).
