# Documentación Interna de Agent Blueprint

Este directorio (`docs/`) contiene la documentación viva, las decisiones de diseño y el registro de evolución del propio repositorio **Agent Blueprint**. 

> [!NOTE]
> Esta documentación está destinada a mantener y hacer evolucionar la plantilla base. Cuando se crea un nuevo proyecto derivado mediante `skeleton/BOOTSTRAP.md`, dicho proyecto recibe su propia carpeta `docs/` adaptada a su propio dominio y plataforma.

---

## Un dato vive en un solo sitio

Para evitar duplicidades e inconsistencias en la gobernanza de la plantilla, cada tipo de información reside exclusivamente en su fuente de la verdad:

| Dimensión / Información | Ubicación canónica | Descripción |
| :--- | :--- | :--- |
| **Roadmap y Fases de la Plantilla** | [`docs/plan/roadmap.md`](plan/roadmap.md) | Estado oficial de versiones (`v0.1.0`, `v0.2.0`, etc.) y reglas de avance. |
| **Especificación de Fase Actual** | [`docs/plan/fases/fase-01-nucleo-y-perfil-movil.md`](plan/fases/fase-01-nucleo-y-perfil-movil.md) | Alcance, criterios de aceptación y checklist de la Fase 1. |
| **Guía de Creación de Proyectos** | [`docs/guias/crear-proyecto.md`](guias/crear-proyecto.md) | Paso a paso detallado para inicializar un nuevo proyecto desde esta plantilla. |
| **Arquitectura de la Plantilla** | [`docs/arquitectura/overview.md`](arquitectura/overview.md) | Modelo de 3 piezas: Raíz de gobernanza, `skeleton/` y `profiles/`. |
| **Registro de Decisiones (ADR)** | [`docs/arquitectura/decisiones/`](arquitectura/decisiones/) | Registro inmutable de decisiones metodológicas y estructurales del blueprint. |
| **Historial de Versiones** | [`docs/CHANGELOG.md`](CHANGELOG.md) | Registro cronológico de cambios, mejoras y correcciones por versión. |
| **Catálogo de Perfiles** | [`profiles/README.md`](../profiles/README.md) | Inventario de perfiles soportados y guía para crear nuevos perfiles de plataforma. |

---

## Estructura de este directorio

```
docs/
├── README.md                          # Este índice central
├── CHANGELOG.md                       # Historial de cambios de agent-blueprint
├── guias/
│   └── crear-proyecto.md              # Guía paso a paso para inicializar nuevos proyectos
├── plan/
│   ├── roadmap.md                     # Roadmap general de evolución de la plantilla
│   └── fases/
│       └── fase-01-nucleo-y-perfil-movil.md # Detalle y criterios de la Fase 1
└── arquitectura/
    ├── overview.md                    # Visión técnica del sistema de 3 capas
    └── decisiones/
        └── 0001-arquitectura-nucleo-y-perfiles.md # ADR inicial de diseño
```

---

## Reglas para evolucionar la plantilla

1. **La plantilla se gobierna con sus propias reglas**: Toda modificación sobre `agent-blueprint` sigue el ciclo de ramas Git (`feature/`, `fix/` hacia `develop`, y releases etiquetados a `main`) y la verificación estricta de documentos.
2. **Compatibilidad hacia downstream**: Toda mejora en `skeleton/` debe preservar la simplicidad del bootstrap para que iniciar un proyecto nuevo continúe siendo una experiencia guiada, rápida y sin fricción.
3. **Desacoplamiento de perfiles**: Las reglas universales (Git, Gentle AI, RDD/ODD) deben permanecer en `skeleton/`, mientras que las particularidades de plataforma deben residir exclusivamente en `profiles/`.
