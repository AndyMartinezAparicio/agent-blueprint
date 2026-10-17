# Registro de Cambios (Changelog)

Todos los cambios notables realizados en este proyecto (**Agent Blueprint**) se registrarán cronológicamente en este documento.

El formato se basa en [Keep a Changelog](https://keepachangelog.com/es-ES/1.1.0/) y este proyecto adhiere al versionado semántico [Semantic Versioning](https://semver.org/lang/es/).

---

## [0.1.0] - 2026-10-18

### Añadido
- **Arquitectura de 3 piezas**: Separación clara entre gobernanza de la plantilla (raíz y `docs/`), esqueleto base universal (`skeleton/`) y catálogo de perfiles especializados (`profiles/`).
- **Esqueleto Universal (`skeleton/`)**:
  - `BOOTSTRAP.md`: Protocolo interactivo guiado por IA para inicializar un nuevo proyecto mediante entrevista estructurada, selección de plataforma e inyección de perfiles.
  - `AGENTS.md`: Manual universal para agentes con filosofía Gentle AI, gobernanza Git estricta (ramas `develop`, `feature/*`, `fix/*`, `release/*`, `main`), desarrollo RDD/ODD y ciclo de vida de tareas.
  - Estructura documental inicial (`docs/vision.md`, `docs/plan/roadmap.md`, `docs/arquitectura/overview.md`, `docs/requerimientos/sistema.md`, `docs/desarrollo.md`).
- **Perfil Móvil Tienda (`profiles/mobile-flutter-store.md`)**:
  - Perfil completo para aplicaciones Flutter destinadas a Google Play y App Store, destilado de las mejores prácticas de *Purge*.
  - Reglas de cumplimiento de políticas de Google Play (permisos granulares, almacenamiento scoped, ciclo de vida, prevención de rechazos).
  - Atributos de calidad: rendimiento a 60/120 fps, paginación por lotes en memoria, soporte TalkBack/Semantics y áreas táctiles mínimas de 48 dp.
  - Restricciones de entorno Windows sin emulador (despliegue exclusivo en dispositivo físico por USB).
  - Comandos pre-commit: `flutter analyze`, `flutter test` y `./gradlew.bat :app:testDebugUnitTest`.
  - Skills recomendadas para agentes en Flutter.
- **Plantilla de Perfiles (`profiles/_TEMPLATE-profile.md`)**: Molde formal para crear futuros perfiles (Web, Desktop, Backend) con secciones canónicas.
- **Documentación Interna de Agent Blueprint (`docs/`)**:
  - `docs/README.md` con mapa canónico "Un dato vive en un solo sitio".
  - `docs/plan/roadmap.md` con las 4 fases de evolución del blueprint.
  - `docs/plan/fases/fase-01-nucleo-y-perfil-movil.md` con alcance y criterios de la versión `v0.1.0`.
  - `docs/arquitectura/overview.md` con diagramas de flujo y ciclo de vida.
  - `docs/arquitectura/decisiones/0001-arquitectura-nucleo-y-perfiles.md` formalizando la decisión arquitectónica fundamental.
