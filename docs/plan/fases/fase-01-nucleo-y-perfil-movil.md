# Fase 1 (v0.1.0) — Núcleo universal, esqueleto base y perfil Móvil (Flutter / Google Play)

| Metadato | Valor |
| :--- | :--- |
| **Versión** | `v0.1.0` |
| **Estado** | **Aprobada** |
| **Fecha de Aprobación** | 2026-10-18 |
| **Documento Rector** | [`docs/plan/roadmap.md`](../roadmap.md) |

---

## Objetivo

Diseñar y materializar el núcleo universal de **Agent Blueprint**, desacoplando la exitosa metodología de trabajo asistido por IA construida en el proyecto *Purge* en una arquitectura modular de 3 componentes:
1. Gobernanza interna de la plantilla.
2. Esqueleto base universal (`skeleton/`) listo para clonar y arrancar cualquier proyecto de software.
3. Primer perfil de plataforma modular (`profiles/mobile-flutter-store.md`) especializado en desarrollo móvil con Flutter y publicación en tiendas como Google Play.

---

## Alcance

### Incluye
- **Separación arquitectónica raíz vs `skeleton/`**: Creación del espacio `skeleton/` como directorio autocontenido que se copia al crear un proyecto nuevo, manteniendo la raíz libre de código de aplicaciones de ejemplo.
- **Protocolo interactivo `skeleton/BOOTSTRAP.md`**: Guía paso a paso para que un agente de IA configure un nuevo proyecto entrevistando al usuario (nombre, propósito, plataforma, stack, perfil aplicable) y generando la documentación inicial sin inventar supuestos.
- **Manual universal de agentes (`skeleton/AGENTS.md`)**:
  - Filosofía **Gentle AI** (respeto por la intención humana, explicaciones claras, validación antes de cambios invasivos).
  - Gobernanza Git estricta (ramas `develop`, `feature/*`, `fix/*`, `release/*`, `main`; commits convencionales; no commits directos a `main`).
  - Desarrollo guiado por documentación y requerimientos (RDD/ODD).
  - Trazabilidad y no dispersión cognitiva.
- **Estructura base de documentación de proyectos (`skeleton/docs/`)**:
  - Plantillas de visión y roadmap del proyecto (`vision.md`, `roadmap.md`).
  - Plantillas de arquitectura y registro de decisiones (`overview.md`, `decisiones/`).
  - Plantillas de requerimientos (`requerimientos/sistema.md`).
  - Guías de desarrollo y validación (`desarrollo.md`).
- **Perfil de plataforma `profiles/mobile-flutter-store.md`**:
  - Requisitos de políticas de Google Play (permisos mínimos, ciclo de vida, almacenamiento restringido).
  - Atributos de calidad móviles: usabilidad táctil, 60/120 fps, paginación en memoria, TalkBack y accesibilidad.
  - Entorno de desarrollo para Windows sin emulador (despliegue directo en dispositivo físico por USB).
  - Comandos de validación pre-commit Flutter/Android.
- **Plantilla de perfiles `profiles/_TEMPLATE-profile.md`**: Estructura estándar para que futuros desarrollos creen perfiles adicionales con consistencia.
- **Documentación interna del blueprint (`docs/`)**: Roadmap, visión de arquitectura y registro del ADR 0001.

### No incluye
- Código fuente de aplicaciones móviles o backend concretas en el repositorio (el repositorio es una meta-plantilla, no una app).
- Perfiles específicos para Web (`profiles/web-app.md`) o Escritorio (`profiles/desktop-app.md`), los cuales corresponden a las Fases 2 y 3.
- Herramienta CLI automatizada en Node/Rust/Python (en esta fase el bootstrap se realiza mediante el agente de IA interpretando `BOOTSTRAP.md`).

---

## Criterios de Aceptación

Todos los criterios han sido completados y verificados:

- [x] **Separación raíz vs `skeleton/`**:
  - El repositorio separa nítidamente las herramientas de la plantilla (`docs/`, `profiles/`) de la estructura de partida de un nuevo proyecto (`skeleton/`).
  - Copiar el contenido de `skeleton/` a un nuevo repositorio produce una base funcional sin dependencias circulares con `agent-blueprint`.

- [x] **Protocolo `BOOTSTRAP.md`**:
  - `skeleton/BOOTSTRAP.md` define un procedimiento determinista de 5 pasos para inicializar un repositorio nuevo.
  - El protocolo pregunta explícitamente al desarrollador sobre plataforma, arquitectura y reglas operativas, inyectando el perfil correspondiente de `profiles/`.

- [x] **Perfil `mobile-flutter-store.md`**:
  - Integra las lecciones aprendidas de *Purge* sobre permisos sensibles, Google Play Console, paginación de colecciones grandes, pruebas en hardware real y suites de tests.
  - Contiene los comandos pre-commit exactos (`flutter analyze`, `flutter test`, `gradlew testDebugUnitTest`).

- [x] **Gobernanza Git y Gentle AI**:
  - `skeleton/AGENTS.md` y `docs/` prescriben el modelo de ramas Gitflow simplificado (`main`, `develop`, `feature/*`, `fix/*`).
  - Se establecen reglas contra suposiciones no consultadas, mutaciones destructivas no solicitadas y generación de código sin pruebas.

- [x] **Documentación arquitectónica interna**:
  - Se genera `docs/arquitectura/overview.md` y el ADR `0001-arquitectura-nucleo-y-perfiles.md` justificando la decisión de diseño.
  - Se formaliza `docs/CHANGELOG.md` con la versión inicial `v0.1.0`.
