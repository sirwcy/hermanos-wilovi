# Hermanos Wilovi — Proyecto AV y WD

## Descripción general
Aplicación web de un solo archivo (`hermanos-wilovi.html`) para acompañar el alcance de objetivos, metas y logros personales de Williams David y Ana Victoria, bajo la supervisión de Williams Contreras (padre/administrador). Sin framework, vanilla JS + HTML + CSS puro.

---

## Arquitectura

- **Un solo archivo**: `hermanos-wilovi.html` contiene todo el HTML, CSS y JS.
- **Persistencia**: `localStorage` con clave `wilovi_state`.
- **Sin dependencias externas** (iconos via Unicode/emoji, sin librerías externas).

---

## Usuarios iniciales

| Nombre             | Username           | Clave | Rol           |
|--------------------|-------------------|-------|---------------|
| Williams Contreras | williams.contreras | 123   | Administrador |
| Williams David     | williams.david     | 123   | Ejecutor      |
| Ana Victoria       | ana.victoria       | 123   | Ejecutor      |

---

## Roles y permisos

| Rol           | Descripción |
|---------------|-------------|
| Administrador | Acceso total: gestión de usuarios, objetivos de todos, configuración |
| Padre         | Lectura de objetivos de los usuarios que se le asignen |
| Ejecutor      | Edición de objetivos propios o de usuarios designados |
| Lector        | Solo lectura de objetivos de usuarios que se le asignen |

---

## Estructura de datos principal

```
state = {
  users: [
    { id, name, username, password, role, canAccessUsers: [userId, ...] }
  ],
  objectives: [
    {
      id, title, description, ownerId, progress,
      subtasks: [
        { id, title, description, progress, subtasks: [...] }  // recursivo
      ]
    }
  ]
}
```

---

## Módulos de la app

1. **Login** — pantalla de inicio con usuario y clave.
2. **Dashboard** — resumen de objetivos por usuario (según rol).
3. **Objetivos** — árbol recursivo de objetivos y subtareas, con progreso.
4. **Admin Usuarios** — solo Administrador: CRUD de usuarios, asignación de roles y accesos.

---

## Reglas de desarrollo

- Siempre editar `hermanos-wilovi.html` como única fuente.
- No romper la persistencia en `localStorage`.
- No introducir dependencias externas.
- Respetar los permisos por rol en toda operación de lectura/escritura.
- El progreso de un nodo con hijos se calcula como promedio de sus hijos.
- El progreso de un nodo hoja es manual (slider 0–100).
