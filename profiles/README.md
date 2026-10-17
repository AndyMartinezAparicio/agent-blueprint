# Catálogo de Perfiles de Plataforma

Este directorio (`profiles/`) contiene los **perfiles de plataforma y stack técnico** de **Agent Blueprint**.

---

## ¿Qué es un perfil de plataforma?

Un perfil es un módulo de conocimiento especializado que condensa las reglas técnicas, normativas y de calidad que son propias de un ecosistema específico (por ejemplo, aplicaciones móviles para Google Play, aplicaciones web con SSR, o software de escritorio nativo).

El núcleo universal del blueprint (`skeleton/AGENTS.md`) define **cómo** colaboran humanos y agentes (Git, RDD, Gentle AI, flujo de trabajo). Un perfil de plataforma define **qué reglas técnicas y restricciones normativas** aplican a esa tecnología concreta.

---

## Cómo lo utiliza `skeleton/BOOTSTRAP.md`

Cuando se crea un nuevo proyecto copiando la carpeta `skeleton/`, el agente de IA ejecuta el protocolo interactivo descrito en `BOOTSTRAP.md`:

1. **Entrevista inicial**: El agente pregunta al desarrollador qué tipo de producto construirá, en qué plataforma operará y qué stack utilizará.
2. **Selección del perfil**: Si el proyecto coincide con un perfil existente (por ejemplo, app Flutter para Android/iOS), el agente consulta el archivo correspondiente en este directorio (`profiles/mobile-flutter-store.md`).
3. **Inyección en el nuevo proyecto**: El agente extrae las secciones del perfil y las transfiere a los documentos pertinentes del nuevo proyecto:
   - Las reglas transversales y comandos pre-commit se añaden al `AGENTS.md` y `desarrollo.md` del nuevo proyecto.
   - Las políticas de plataforma y requisitos de privacidad se integran en `docs/requerimientos/sistema.md`.
   - Los atributos de calidad y skills sugeridas se reflejan en la arquitectura y configuración del entorno.
4. **Desconexión**: Una vez completado el bootstrap, el nuevo proyecto ya no necesita consultar este directorio; toda la configuración vive integrada dentro de su propio repositorio.

---

## Perfiles disponibles

| Archivo de Perfil | Plataforma / Stack | Ámbito de aplicación | Estado |
| :--- | :--- | :--- | :--- |
| [`mobile-flutter-store.md`](mobile-flutter-store.md) | **Flutter / Android & iOS** | Apps móviles para Google Play / App Store con requisitos de permisos, ciclo de vida, rendimiento en hardware y pruebas en dispositivo real. | **Activo (v0.1.0)** |
| `web-app.md` | **Web SPA / Fullstack** | Aplicaciones web modernas con SEO, accesibilidad web, Core Web Vitals y seguridad HTTP. | *Planificado (Fase 2)* |
| `desktop-app.md` | **Desktop (Flutter / Electron / Nativo)** | Software para Windows, macOS y Linux con integración al sistema de ventanas y archivos locales. | *Planificado (Fase 3)* |

---

## Cómo crear un nuevo perfil de plataforma

Para añadir soporte para una nueva plataforma o stack, sigue estos pasos:

1. **Copiar la plantilla base**:
   Copia el archivo [`_TEMPLATE-profile.md`](_TEMPLATE-profile.md) con el nombre de tu perfil en minúsculas y separado por guiones (por ejemplo: `web-app.md`, `desktop-app.md` o `backend-fastapi.md`).

2. **Rellenar las secciones canónicas obligatorias**:
   - **Reglas Transversales de Plataforma**: Políticas de la tienda/ecosistema, estándares de la industria, directrices de compatibilidad.
   - **Privacidad y Seguridad por Defecto**: Permisos mínimos, almacenamiento local, protección de datos y manejo de credenciales.
   - **Atributos de Calidad Específicos**: Métricas de rendimiento (FPS, latencia, memoria), usabilidad, fiabilidad y accesibilidad adaptadas a la plataforma.
   - **Entorno de Desarrollo y Restricciones**: Reglas sobre emuladores, hardware de pruebas, SDKs permitidos y gestión de espacio en disco.
   - **Comandos de Validación Pre-Commit**: Comandos deterministas de linter, compilación, tipos y tests que deben pasar en verde al 100%.
   - **Skills Recomendadas para el Agente**: Herramientas o skills del agente más útiles para ese ecosistema.

3. **Registrar el nuevo perfil**:
   - Añade el perfil a la tabla de perfiles en este archivo (`profiles/README.md`).
   - Actualiza el listado en `skeleton/BOOTSTRAP.md` para que el agente lo ofrezca durante la entrevista de inicialización.
   - Si forma parte de una fase formal del roadmap (como la Fase 2 para Web), actualiza `docs/plan/roadmap.md` y `docs/CHANGELOG.md`.
