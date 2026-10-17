# ADR 0001: Arquitectura de núcleo universal, esqueleto y perfiles modulares

| Metadato | Valor |
| :--- | :--- |
| **Estado** | **Aceptado** |
| **Fecha** | 2026-10-18 |
| **Autores** | Andy & Agente Arquitecto |
| **Decisores** | Equipo de desarrollo |

---

## Contexto

Durante el desarrollo de *Purge* (una aplicación móvil en Flutter con políticas estrictas de Google Play, ciclo de vida Android y gestión exhaustiva de archivos multimedia), se consolidó un sistema de trabajo altamente eficaz basado en:
- Directrices rigurosas de comportamiento para agentes de IA (**Gentle AI**).
- Gobernanza de ramas Git limpia y estricta (sin commits descontrolados, flujo `develop`/`feature`/`main`).
- Metodología orientada a requerimientos y documentación canónica (ODD/RDD).
- Validación continua pre-commit para garantizar cero regresiones.

Al plantear nuevos proyectos futuros (tanto móviles como aplicaciones web, herramientas de escritorio o microservicios), surgió la necesidad evidente de reutilizar esta metodología y su infraestructura documental. Sin embargo, clonar directamente el repositorio de *Purge* o mantener una plantilla monolítica presentaba serios inconvenientes:
1. **Contaminación conceptual**: Un proyecto web o de escritorio no debe heredar directrices sobre `READ_MEDIA_IMAGES`, el ciclo de vida de actividades de Android ni comandos específicos de `gradlew`.
2. **Duplicación y divergencia**: Si cada nuevo proyecto copia y modifica un monolito, las mejoras en las reglas de agentes o en la metodología Git descubiertas en un proyecto no benefician fácilmente a los demás.
3. **Falta de evolución propia**: Se requería un mecanismo donde la propia plantilla pudiera ser mantenida, versionada y mejorada siguiendo el mismo flujo de calidad que los proyectos finales.

---

## Decisión

Se decide estructurar el repositorio **Agent Blueprint** en tres piezas desacopladas:

1. **Raíz de gobernanza (`/`, `docs/`)**:
   - Gestiona el ciclo de vida y versiones de la propia plantilla mediante su propio roadmap, especificaciones de fase, ADRs y changelog.
   - Aplica a sí misma las reglas de desarrollo guiado por IA y gobernanza Git.

2. **Esqueleto base universal (`skeleton/`)**:
   - Contiene únicamente los archivos universales agnósticos al stack tecnológico:
     - `BOOTSTRAP.md`: Protocolo interactivo de arranque donde el agente entrevista al desarrollador y configura el proyecto.
     - `AGENTS.md`: Manual universal de colaboración humano-IA, flujo Git, RDD y principios Gentle AI.
     - `docs/`: Estructura documental base para el nuevo proyecto (`vision.md`, `roadmap.md`, `arquitectura/`, etc.).
   - Es el directorio que el desarrollador copia en su nuevo entorno para inicializar un proyecto.

3. **Catálogo de perfiles de plataforma (`profiles/`)**:
   - Módulos de conocimiento técnico y normativo independientes por plataforma/stack.
   - Para la Fase 1, se extrae el conocimiento de *Purge* en el primer perfil oficial: `mobile-flutter-store.md`.
   - Se provee una plantilla estandarizada (`_TEMPLATE-profile.md`) para habilitar la futura creación de perfiles (`web-app.md`, `desktop-app.md`, `backend-api.md`).
   - Durante la ejecución de `BOOTSTRAP.md`, el agente lee el perfil correspondiente e inyecta sus restricciones, atributos de calidad y comandos pre-commit en los archivos definitivos del proyecto.

---

## Consecuencias

### Positivas
- **Máxima reutilización**: Las reglas operativas de agentes y Git residen en un solo núcleo (`skeleton/AGENTS.md`), evitando reinventar la rueda en cada inicio de proyecto.
- **Cero ruido en proyectos downstream**: Cada proyecto recibe únicamente las instrucciones pertinentes a su plataforma (un backend no ve reglas de Android; una app móvil no ve directrices de SEO).
- **Escalabilidad de plataformas**: Incorporar soporte para un nuevo ecosistema (Fases 2 y 3: Web y Escritorio) requiere únicamente añadir un nuevo archivo a `profiles/`, sin alterar el esqueleto base.
- **Evolución ordenada**: La plantilla se auto-mantiene con control de versiones semántico (`v0.1.0`, `v0.2.0`), changelog estandarizado y roadmap auditable.

### Negativas / Compromisos
- Requiere un paso explícito de inicialización (`BOOTSTRAP.md`) antes de comenzar a escribir código en el proyecto downstream, donde el agente debe leer el perfil y realizar la inyección de directrices. Este compromiso se considera positivo, pues garantiza que el proyecto comience con una visión y requerimientos claros y validados con el humano.
