# 💡 Decisiones de Diseño

## Punto de partida — análisis de la organización

Antes de crear una sola base de datos, se realizó un análisis completo de Rebs como organización:

- Mapeo de todos los roles y sus responsabilidades reales
- Identificación de los flujos de información entre departamentos
- Detección de fricciones operativas — dónde se perdía tiempo y datos
- Análisis de las herramientas existentes (Salesforce, hojas de cálculo, email)

**Conclusión del análisis:** la organización operaba con información fragmentada en múltiples herramientas sin conexión entre sí. Los datos no fluían — se copiaban manualmente de un sitio a otro.

---

## Decisión 1 — Una sola fuente de verdad

Toda la información de Rebs vive en un único ecosistema. No hay datos duplicados en herramientas separadas.

```
❌ Antes
Alumnos → Excel
Tareas → Email / WhatsApp
Calidad → Google Forms sueltos
Equipo → Carpetas locales
Contratos → Papel / Email

✅ Después
Todo → VElite (46+ BDs interconectadas)
```

**Impacto:** cualquier miembro del equipo puede encontrar cualquier información en un único lugar, con permisos que garantizan que solo ve lo que le corresponde.

---

## Decisión 2 — Estaciones de trabajo personales

El ecosistema completo tiene 46+ bases de datos y 150+ vistas. Exponer eso directamente al equipo operativo sería contraproducente.

La solución fue crear una **Estation personal** para cada rol — un panel de entrada que filtra el ecosistema al contexto exacto de esa persona.

```
Sistema completo          Estation de Empleado Operativo
46+ BDs        →          · Mis tareas de hoy
150+ vistas               · Mis hitos activos
27+ paneles               · Mi programa asignado
                          · Mi rendimiento
```

**Resultado:** el equipo trabaja con foco total. La complejidad del sistema es invisible para quien no la necesita.

---

## Decisión 3 — [SYSTEM] como capa invisible

Toda la infraestructura técnica — arquitectura, seguridad, credenciales, administración — está aislada en un módulo separado con acceso restringido.

El equipo operativo nunca ve ni necesita ver cómo está construido el sistema que usa. Solo ve su Estation y los paneles de su área.

**Analogía técnica:** es el equivalente a separar el código fuente del producto final. El usuario usa la aplicación sin ver ni tocar el backend.

---

## Decisión 4 — Relaciones bidireccionales en lugar de duplicación

Cuando un dato necesita aparecer en varios contextos, se crea una **relación bidireccional** entre bases de datos — no se copia el dato.

```
❌ Sin relaciones
DB_Alumnos → campo "Encuesta" (texto manual, desactualizado)
DB_Encuestas → campo "Alumno" (texto manual, desactualizado)

✅ Con relación bidireccional
DB_Alumnos ←→ DB_Encuestas
Actualizar en un lado → se refleja automáticamente en el otro
```

**17 relaciones bidireccionales** activas en el sistema. Cero duplicación de datos críticos.

---

## Decisión 5 — Diseño no destructivo

Ningún dato se elimina del sistema — se archiva. Esto garantiza:

- Historial completo y auditable
- Posibilidad de recuperar cualquier registro
- Trazabilidad de decisiones y cambios

Las BDs tienen campos de estado (`Activo · Archivado · Pendiente`) en lugar de borrado permanente.

---

## Decisión 6 — Escalabilidad por diseño

El sistema fue diseñado para crecer sin rediseño:

- **Nuevo empleado** → crear ficha + asignar permisos + crear Estation. 30 minutos.
- **Nuevo programa académico** → crear BD + vincular relaciones existentes. Sin tocar el resto.
- **Nueva área de negocio** → añadir módulo al nivel correspondiente. La arquitectura base no cambia.

---

## Resultado operativo

| Problema inicial | Solución implementada |
|-----------------|----------------------|
| Información fragmentada en múltiples herramientas | Una sola fuente de verdad — 46+ BDs interconectadas |
| Equipo sin visibilidad de su trabajo diario | Estaciones personales por rol |
| Datos duplicados y desactualizados | 17 relaciones bidireccionales |
| Sin control de acceso granular | Sistema de permisos por subpágina y rol |
| Infraestructura mezclada con operaciones | [SYSTEM] como capa técnica aislada |
| Coste elevado de herramientas de gestión | Notion Teams — 10€/mes para todo el equipo |

---

## Nota sobre adopción

El sistema está diseñado y documentado para uso de todo el equipo. La adopción organizacional depende de la voluntad de cambio interna — un factor humano fuera del alcance técnico del proyecto. El arquitecto del sistema lo usó en producción real para gestionar 40+ tareas simultáneas durante las prácticas, validando su operatividad en condiciones reales.
