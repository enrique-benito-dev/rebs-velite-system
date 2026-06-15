# 🔐 Sistema de Permisos y Acceso

## Filosofía de control de acceso

VElite implementa un modelo de **acceso mínimo necesario** — cada rol ve exactamente lo que necesita para su función y nada más. Esto elimina el ruido informativo, protege datos sensibles y permite que el sistema escale sin reconfiguración cada vez que entra un nuevo miembro.

---

## Arquitectura de permisos

```
[SYSTEM] → Panel de Bases de Datos
                    │
        ┌───────────┴───────────┐
        │                       │
   Subpágina BD 1          Subpágina BD 2   ···
        │                       │
   Permisos propios        Permisos propios
   por rol                 por rol
```

Cada base de datos vive en su propia subpágina dentro del Panel de BD. Los permisos se asignan a nivel de subpágina — no a nivel de sistema completo. Esto permite control granular sin complejidad de administración.

---

## Roles del sistema

| Rol | Perfil | Acceso |
|-----|--------|--------|
| **Admin** | Dirección / IT | Total — todas las BDs, seguridad completa, credenciales |
| **Notion Manager** | Arquitecto del sistema (EB) | Todas las BDs operativas — edición completa |
| **Director de Área** | Responsable de departamento | BDs de su área + edición de las propias |
| **Empleado Operativo** | Equipo de trabajo | Tareas, Hitos, Equipo — solo sus registros |
| **Colaborador Externo** | Partners, proveedores | Solo la BD de su proyecto específico |

---

## Protocolo de onboarding

Cuando entra un nuevo miembro al equipo, el proceso es:

```
1. Crear ficha en DB_Equipo con rol asignado
2. Invitar al workspace de Notion con permisos base
3. Asignar acceso en cada subpágina de BD según rol
4. Crear su Estation personal con sus filtros y vistas
5. Briefing de 15 min sobre navegación del sistema
```

**Tiempo estimado de onboarding técnico:** 30 minutos.

---

## Protocolo de offboarding

Cuando un miembro sale de la organización:

```
1. Revocar acceso en todas las subpáginas de BD
2. Reasignar sus tareas e hitos activos
3. Archivar su Estation personal
4. Actualizar DB_Equipo con fecha de salida
5. Auditoría de accesos — verificar que no quedan permisos activos
```

---

## Seguridad de la infraestructura

El módulo **[SYSTEM] → Panel de Seguridad** contiene dos capas:

**Capa pública — 11 protocolos para todo el equipo:**
- Protocolo 1 — Gestión de contraseñas
- Protocolo 2 — Uso de dispositivos corporativos
- Protocolo 3 — Manejo de datos de alumnos (RGPD)
- Protocolo 4 — Entrada de nuevos empleados
- Protocolo 5 — Salida de empleados
- Protocolos 6-11 — Incidencias, backups y continuidad operativa

**Capa restringida — solo admin:**
- Credenciales de infraestructura
- Registro de incidentes
- Auditoría de accesos
- Configuración técnica del sistema

---

## Escalabilidad del modelo

Añadir un nuevo programa, departamento o proyecto al ecosistema es:

```
1. Crear las BDs necesarias en Panel de BD
2. Establecer relaciones con BDs existentes
3. Crear vistas en los paneles correspondientes
4. Asignar permisos al equipo involucrado
```

No requiere rediseño del sistema. La arquitectura base absorbe el crecimiento.

> ⚠️ Las credenciales, nombres de usuario y configuraciones específicas de la infraestructura de Rebs no están incluidas en este repositorio.
