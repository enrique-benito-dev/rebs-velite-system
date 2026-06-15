# 🏗️ Arquitectura del Sistema

## Filosofía de diseño

VElite parte de un análisis completo de la organización — personas, procesos, flujos de información y necesidades por rol — antes de escribir una sola base de datos. El resultado es un sistema que refleja cómo trabaja Rebs realmente, no cómo debería trabajar en teoría.

**Principio central:** cada capa del sistema tiene un propósito claro y sabe dónde empieza y dónde termina.

---

## Estructura de 5 niveles

```
NIVEL 0 — Entrada
└── 🏠 Home
        Panel de orientación diaria. Buzón de urgentes,
        acceso a estaciones personales y estado del día.
        Punto de entrada para todos los roles.

NIVEL 1 — Operaciones
└── 📘 Operaciones
        El motor del trabajo diario:
        ├── CRM — seguimiento comercial y pipeline de alumnos
        ├── Forecasting — proyección de matrículas
        ├── Marketing — campañas y activos de comunicación
        ├── Academia y Calidad — gestión académica y encuestas
        ├── Tareas e Hitos — trabajo del equipo
        └── Buzón — entrada centralizada de urgentes

NIVEL 2 — Conocimiento
└── 🎯 Especialización
        Capital intelectual y recursos del equipo:
        ├── Biblioteca de IA — prompts, herramientas y casos de uso
        ├── Activos Estratégicos — documentación y recursos clave
        └── Formación interna

NIVEL 3 — Dirección
└── ⌛ Dirección y Estrategia
        Capa de decisión:
        ├── Indicadores clave de negocio
        ├── Informes de rendimiento
        └── Visión estratégica y planificación

NIVEL 4 — Infraestructura
└── 🔧 [SYSTEM]
        Núcleo técnico invisible para el equipo operativo:
        ├── Panel de Bases de Datos — 46+ BDs categorizadas
        ├── Panel de Arquitectura — documentación técnica completa
        ├── Panel de Seguridad — 11 protocolos + credenciales admin
        ├── Panel Admin — contratos, trámites, configuración
        └── Rama Maestra — mapa relacional completo v3.0
```

---

## Red de relaciones

El sistema cuenta con **17 relaciones bidireccionales** entre bases de datos. Esto significa que un registro en una BD puede verse y actualizarse desde múltiples contextos sin duplicar datos.

Ejemplos de relaciones clave:

| BD origen | BD destino | Propósito |
|-----------|-----------|-----------|
| Alumnos | Encuestas de Calidad | Vincular valoraciones al alumno |
| Equipo | Tareas | Asignación y seguimiento por persona |
| Proyectos | Hitos | Control de avance por entregable |
| Activos Estratégicos | Sistemas Activos | Trazabilidad de recursos digitales |
| Automatizaciones | Sistemas Activos | Registro de herramientas en producción |

---

## Estaciones de trabajo personales

Cada miembro del equipo tiene una **Estation** — un panel de entrada personalizado que filtra el ecosistema a su contexto de trabajo.

```
Ecosistema completo (46+ BDs · 150+ vistas)
            ↓
    Estation personal
            ↓
Solo lo relevante para ese rol:
    · Sus tareas del día
    · Sus hitos activos
    · Sus programas o alumnos asignados
    · Sus métricas de rendimiento
```

**Resultado:** el equipo opera con foco total sin necesidad de navegar el sistema completo.

---

## Flujo de datos principal

```
Entrada de datos
    │
    ├── Buzón (urgentes) ──────────────────────────────┐
    │                                                  │
    ├── CRM (alumnos/leads) ─────────────────────────┐│
    │                                                 ││
    └── Operaciones (tareas/hitos/proyectos) ────────┐││
                                                     │││
                                                     ▼▼▼
                                          Bases de datos relacionales
                                                     │
                                    ┌────────────────┼────────────────┐
                                    ▼                ▼                ▼
                              Estaciones        Dirección         [SYSTEM]
                              personales        y Estrategia      Auditoría
```

---

## Evolución del sistema

| Versión | Fecha | Cambios principales |
|---------|-------|---------------------|
| v1.0 | Oct 2025 | Estructura inicial — módulos base y primeras BDs |
| v2.0 | Feb 2026 | Estaciones personales · Sistema de permisos por rol |
| v3.0 | May 2026 | [SYSTEM] completo · Rama Maestra · 17 relaciones bidireccionales · 150+ vistas |
