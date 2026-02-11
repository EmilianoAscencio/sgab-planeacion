# Descripción del Proyecto

## Objetivo del sistema
El Sistema de Gestión Académica Básico (SGAB) tiene como objetivo apoyar la administración académica de una institución educativa mediante una plataforma web que permita gestionar alumnos, materias, calificaciones y usuarios de manera centralizada, organizada y confiable.

El sistema busca reducir errores administrativos, mejorar el acceso a la información y facilitar los procesos académicos cotidianos.

## Usuarios principales
- **Administrador Académico:** Responsable de la gestión general del sistema, incluyendo usuarios, alumnos y materias.
- **Docente:** Encargado de registrar y consultar calificaciones de las materias asignadas.
- **Alumno:** Usuario que consulta su información académica, principalmente materias inscritas y calificaciones.

## Problema que resuelve
En muchos entornos educativos, la información académica se maneja mediante archivos dispersos o procesos manuales, lo que genera inconsistencias, duplicidad de datos y dificultad para mantener la información actualizada.

El SGAB centraliza la información académica en un solo sistema, permitiendo un acceso controlado, organizado y confiable para cada tipo de usuario.

## Suposiciones iniciales
- El sistema será utilizado por una institución educativa de tamaño pequeño o mediano.
- Los usuarios cuentan con acceso a internet y conocimientos básicos de navegación web.
- El sistema será accedido únicamente mediante navegadores web modernos.
- No se consideran integraciones con sistemas externos en la primera versión.

## Diagrama de contexto (ASCII)
[ Alumno ] --------> [ Docente ] ----> [SGAB ] ----> [ Base de Datos ] ----> [Administrador]