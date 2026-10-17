# Roadmap de Evolución de Agent Blueprint

Este documento establece la hoja de ruta para el desarrollo y perfeccionamiento de **Agent Blueprint** como repositorio y metodología base para proyectos asistidos por Inteligencia Artificial.

---

## Estado general del proyecto

| Versión | Fase | Enfoque principal | Estado | Fecha de cierre |
| :--- | :--- | :--- | :--- | :--- |
| **v0.1.0** | **Fase 1** | Núcleo universal, esqueleto base y perfil Móvil (Flutter / Google Play) | **Aprobada** | 2026-10-18 |
| **v0.2.0** | **Fase 2** | Perfil Web App (Frontend / Fullstack) | **Pendiente** | — |
| **v0.3.0** | **Fase 3** | Perfil Aplicación de Escritorio | **Pendiente** | — |
| **v0.4.0** | **Fase 4** | Catálogo de Skills reutilizables y mejoras de Bootstrap | **Pendiente** | — |

---

## Detalle de Fases

### Fase 1 (v0.1.0) — Núcleo universal, esqueleto base y perfil Móvil
- **Objetivo**: Extraer y formalizar la metodología probada en *Purge* en una plantilla desacoplada de 3 piezas: Raíz de mantenimiento, `skeleton/` genérico para nuevos proyectos y `profiles/` modulares por plataforma.
- **Entregables**:
  - Estructura universal `skeleton/` con protocolo interactivo `BOOTSTRAP.md`.
  - Manual de agentes universales (`skeleton/AGENTS.md`) con gobernanza Git, filosofía Gentle AI y desarrollo guiado por requerimientos (RDD/ODD).
  - Perfil de plataforma inicial: `profiles/mobile-flutter-store.md` (Flutter, Google Play, Android, privacidad, rendimiento en dispositivo).
  - Plantilla de perfiles `profiles/_TEMPLATE-profile.md` y guía de uso.
  - Documentación de arquitectura interna y ADR inicial.
- **Estado**: **Aprobada** (2026-10-18).
- **Detalle completo**: [`docs/plan/fases/fase-01-nucleo-y-perfil-movil.md`](fases/fase-01-nucleo-y-perfil-movil.md).

---

### Fase 2 (v0.2.0) — Perfil Web App (Frontend / Fullstack)
- **Objetivo**: Desarrollar el perfil oficial para aplicaciones web modernas (SPA, SSR o Fullstack) garantizando el mismo rigor de gobernanza.
- **Alcance previsto**:
  - Perfil `profiles/web-app.md`.
  - Reglas transversales: SEO, Core Web Vitals, PWA, empaquetado, responsive design multiplataforma web.
  - Reglas de seguridad web: CORS, CSP, gestión de tokens, sanitización XSS/CSRF.
  - Comandos pre-commit para linter, TypeScript check y pruebas de integración/componentes.
- **Condición de inicio**: Se definirá e implementará al construir el primer proyecto web real con esta metodología.
- **Estado**: **Pendiente**.

---

### Fase 3 (v0.3.0) — Perfil Aplicación de Escritorio
- **Objetivo**: Definir el perfil oficial para aplicaciones de escritorio (Flutter Desktop, Electron, Tauri, .NET/C# o similar).
- **Alcance previsto**:
  - Perfil `profiles/desktop-app.md`.
  - Reglas transversales: Empaquetado nativo (MSIX, DMG, AppImage), integraciones con sistema operativo (notificaciones nativas, bandejas de sistema, menús de ventana).
  - Gestión de archivos en sistema local, cuotas de disco y portabilidad multiplataforma.
- **Condición de inicio**: Se definirá e implementará al construir el primer proyecto de escritorio real con esta metodología.
- **Estado**: **Pendiente**.

---

### Fase 4 (v0.4.0) — Catálogo de Skills reutilizables y mejoras de Bootstrap
- **Objetivo**: Estandarizar una biblioteca de skills reutilizables para agentes y optimizar la automatización del proceso de bootstrap.
- **Alcance previsto**:
  - Catálogo centralizado de skills empaquetadas (análisis de contratos de API, generación de suites de tests, auditorías de accesibilidad).
  - Scripts opcionales de inicialización desatendida o CLI interactivo complementario al protocolo `BOOTSTRAP.md`.
- **Estado**: **Pendiente**.

---

## Reglas de avance y gobernanza de fases

Agent Blueprint opera bajo las mismas reglas de integridad y trazabilidad que exige a los proyectos derivados:

1. **Desarrollo en rama de fase**: Cada fase se implementa en ramas temáticas (`feature/...`, `docs/...`) derivadas de `develop`.
2. **Revisión y Aprobación**: Para dar por aprobada una fase, todos sus criterios de aceptación deben verificarse positivamente y reflejarse con `[x]` en el documento de fase correspondiente dentro de `docs/plan/fases/`.
3. **Fusión en `develop` y Release en `main`**:
   - Al completar la fase, se integran los cambios en `develop`.
   - Se crea una Pull Request de release hacia `main`.
   - Tras la fusión en `main`, se crea la etiqueta anotada correspondiente (`git tag -a vX.Y.Z -m "Release vX.Y.Z: ..."`) y se actualiza `docs/CHANGELOG.md`.
4. **Ningún commit directo a `main`**: La rama `main` refleja únicamente versiones estables aprobadas.
