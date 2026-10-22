# Protocolo de Inicialización (BOOTSTRAP.md) — Día 0

> **INSTRUCCIÓN FUNDAMENTAL PARA EL AGENTE DE IA:**  
> Si el usuario te pide inicializar el proyecto con `BOOTSTRAP.md`, **NO escribas código todavía**.  
> Sigue este protocolo paso a paso haciendo preguntas cortas y concisas, y **espera siempre la aprobación explícita del usuario** antes de escribir o modificar archivos en el repositorio.

Este protocolo guía la transición de un repositorio vacío o plantilla base (`agent-blueprint`) a un proyecto completamente configurado, documentado y listo para desarrollo profesional bajo la metodología de Andy.

> [!NOTE]
> **Alcance del Día 0**: El Día 0 es estrictamente documental y de gobernanza. No se genera lógica de negocio ni se exige que los comandos de compilación o test del stack corran en el Día 0 (estos se activan en la Fase 1 al inicializar el proyecto de código en disco).

---

## Fase 1 — Entrevista de Descubrimiento

Formula al usuario las siguientes **5 preguntas clave** (puedes formularlas en un solo mensaje estructurado o de forma dialogada si el usuario lo prefiere):

1. **Identidad y estructura del proyecto:**
   - ¿Cuál es el nombre del proyecto (`{{NOMBRE_PROYECTO}}`)?
   - ¿En qué subcarpeta vivirá el código fuente (por ejemplo: `app/`, `cliente/`, `src/` o `<nombre_proyecto>/`)?

2. **Visión y propósito:**
   - ¿Qué problema central resuelve la aplicación y quién es el usuario objetivo (público destinatario)?  
     *(Esta respuesta alimentará `docs/producto/vision.md`)*.

3. **Perfil de plataforma y entorno de desarrollo:**
   - ¿Qué perfil o stack técnico se aplicará (por ejemplo: Flutter móvil con publicación en tiendas, React/Web, backend Node/Python, CLI, o perfil personalizado)?
   - ¿Cuáles son las restricciones del entorno del desarrollador (Sistema Operativo, pruebas en dispositivo físico por USB, emulador, navegador web, versiones de herramientas instaladas)?

4. **Alcance de la versión 1.0 y directrices no negociables:**
   - ¿Cuáles son los requisitos funcionales clave de la v1.0 (`RF-01` a `RF-XX`)?
   - ¿Existen principios estrictos de privacidad, modo offline o normativas externas obligatorias (por ejemplo: políticas de Google Play / App Store, RGPD, almacenamiento local sin telemetría)?

5. **Referencia visual y diseño de interfaz:**
   - ¿Se cuenta con capturas o maquetas de referencia (en `design/`, capturas de Stitch/Figma, etc.)?
   - ¿Existe una paleta de colores base, soporte de modo oscuro/claro o tipografía definida?

---

## Fase 2 — Propuesta de Plan de Inicialización

Una vez recibidas las respuestas del usuario, **NO generes los archivos de inmediato**.  
Elabora un resumen ejecutivo de inicialización estructurado que describa cómo quedará configurada la documentación fundacional:

1. **`AGENTS.md`**: Definición del proyecto, comandos del entorno, reglas de plataforma aplicables.
2. **`docs/producto/vision.md`**: Problema, propuesta de valor y usuario ideal.
3. **`docs/producto/requisitos.md`**: Lista inicial de requisitos funcionales (`RF-01..RF-N`) y no funcionales (`RNF-01..RNF-N`).
4. **`docs/arquitectura/overview.md`**: Arquitectura elegida (capas, gestión de estado, dependencias principales).
5. **`docs/arquitectura/decisiones/0001-stack-y-arquitectura-inicial.md`**: Registro de Decisión de Arquitectura (ADR) fundacional justificando la elección tecnológica.
6. **`docs/plan/roadmap.md`**: Desglose en fases (Fase 1: Fundación / MVP base, Fase 2: Funcionalidades núcleo, etc.).
7. **`docs/plan/fases/fase-01-fundacion.md`**: Detalle minucioso de tareas para arrancar la primera fase (Fundación).
8. **`docs/guias/desarrollo.md`**: Comandos locales de compilación, ejecución de tests, linter y formateo.
9. **`design/DESIGN.md`**: Tokens de diseño, archivo central de paleta, sistema de internacionalización y componentes base.
10. **`.claude/skills/project-ui/SKILL.md`**: Skill adaptada a las directrices UI del proyecto.
11. **`.claude/skills/material-design/SKILL.md`**: Skill adaptada con la guía de Material 3 para el proyecto.

> **ALTO:** Presenta esta propuesta al usuario y solicita su confirmación:  
> *"¿Estás de acuerdo con este plan de inicialización o deseas ajustar algún punto antes de escribir los archivos?"*

---

## Fase 3 — Escritura de la Documentación Fundacional

Tras recibir la aprobación explícita del usuario:

1. Rellena todos los marcadores de posición (`{{...}}`) en:
   - `AGENTS.md`
   - `README.md`
   - `design/DESIGN.md`
   - `.claude/skills/project-ui/SKILL.md`
   - `.claude/skills/material-design/SKILL.md`
   - Toda la suite documental en `docs/` (`docs/producto/`, `docs/arquitectura/`, `docs/plan/`, `docs/guias/`).
2. Inyecta fielmente las reglas del perfil seleccionado (por ejemplo, directrices de permisos para Android, políticas de Google Play, o arquitectura offline-first).
3. Asegura que ningún archivo concreto contenga placeholders sin resolver (`{{...}}`).
   > **Exención intencional de plantillas:** Los archivos de plantilla reutilizable (`_TEMPLATE-adr.md`, `_TEMPLATE-fase.md` y `_TEMPLATE-task.md`) conservan sus placeholders intencionalmente para su uso futuro en nuevas decisiones, fases o tareas.
4. **Coherencia de árboles y rutas:** Si el proceso de inicialización se delega en subagentes en paralelo, el árbol de carpetas de `README.md`, `docs/arquitectura/overview.md` y la estructura en disco deben ser 100% idénticos y coherentes.
5. Presenta al usuario un resumen de los archivos creados o actualizados.

---

## Fase 4 — Limpieza e Inicialización de Git

Una vez completada la documentación fundacional:

1. **Solicitar permiso para eliminar `BOOTSTRAP.md`:**  
   Informa al usuario que `BOOTSTRAP.md` ha cumplido su ciclo de vida y solicita autorización para eliminarlo del repositorio.

2. **Proponer los comandos exactos de Git y herramientas:**  
   Presenta al usuario los comandos precisos para arrancar el control de versiones y refrescar el registro de skills:

   ```powershell
   # 1. Inicializar repositorio Git y rama principal
   git init -b main

   # 2. Refrescar registro de skills de Gentle AI (genera/actualiza .atl/skill-registry.md)
   gentle-ai skill-registry refresh

   # 3. Añadir documentación fundacional y realizar el primer commit (incluyendo .atl/skill-registry.md)
   git add .
   git commit -m "docs: inicializar arquitectura y documentacion fundacional"

   # 4. Crear y posicionarse en la rama de trabajo develop
   git checkout -b develop
   ```

3. Espera la confirmación del usuario antes de ejecutar o dar por cerrado el protocolo de inicio.
