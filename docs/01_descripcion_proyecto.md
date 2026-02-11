# Descripción del Proyecto

## Objetivo del sistema
Desarrollar un sistema web que permita gestionar de manera centralizada la información académica de una institución, incluyendo alumnos, materias, calificaciones y usuarios administrativos.

## Usuarios principales
- **Administrador académico**: gestiona usuarios, materias y configuraciones generales.
- **Docente**: registra y consulta calificaciones.
- **Alumno**: consulta sus materias y calificaciones.

## Problema que resuelve
Actualmente, la gestión académica suele realizarse mediante archivos dispersos o sistemas no integrados, lo que provoca errores, duplicidad de información y dificultad para acceder a datos actualizados.

El SGAB busca centralizar la información, mejorar la organización y reducir errores operativos.

## Suposiciones iniciales
- El sistema será utilizado en una institución de tamaño pequeño o mediano.
- Los usuarios tienen conocimientos básicos de uso de sistemas web.
- El sistema se accede desde navegadores modernos.
- No se consideran integraciones con sistemas externos en la primera versión.

## Diagrama de contexto (ASCII)
[ Alumno ] --------> [ Docente ] ----> [SGAB ] ----> [ Base de Datos ] ----> [Administrador]