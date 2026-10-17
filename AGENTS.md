# AGENTS.md — Reglas Universales del Sistema Agent Blueprint

> **Aviso para cualquier Agente de IA (Claude Code, Antigravity, Cursor, OpenCode):**
> Este archivo define las reglas de conducta, flujo de ingeniería y restricciones operativas que debes cumplir con rigor absoluto al operar en este repositorio.

---

## 🎯 Contexto Dual de Operación (Lectura Obligatoria Inmediata)

Antes de iniciar cualquier acción, determina en cuál de los dos contextos estás operando:

1. **Contexto A — Creación / Inicialización de un nuevo proyecto**:
   - Si el usuario solicita inicializar un nuevo proyecto a partir de esta plantilla, **tu foco de trabajo es la carpeta de destino del nuevo proyecto**, NO modificar este repositorio.
   - Debes guiarte por `skeleton/BOOTSTRAP.md` y por los perfiles específicos ubicados en `profiles/` (por ejemplo, `profiles/mobile-flutter-store.md`).
   - Copia la estructura base de `skeleton/` hacia la ubicación designada por el usuario y ejecuta la entrevista guiada Día 0.

2. **Contexto B — Mantenimiento / Ampliación de esta plantilla (`agent-blueprint`)**:
   - Si el usuario solicita mejorar, añadir perfiles, crear skills o evolucionar el blueprint, estás trabajando directamente sobre este repositorio.
   - Debes consultar obligatoriamente `docs/plan/roadmap.md` y seguir las reglas que se detallan a continuación.

---

## 🏛️ Reglas Fundamentales de Ingeniería

### 1. La documentación manda ("Un dato vive en un solo sitio")
- `docs/` es la **única fuente de verdad** funcional, técnica y arquitectónica.
- `design/` manda **únicamente en aspectos visuales** ("Notas del proyecto"): interfaces, maquetas, paletas y componentes estéticos.
- Ningún código o refactorización puede implementarse si contradice o anticipa a la documentación aprobada.
- Si surge una discrepancia o necesidad técnica imprevista, primero se actualiza y aprueba la documentación en `docs/`, y luego se escribe el código.

### 2. Plan antes que código
- Antes de escribir o modificar una sola línea de código, debes presentar un **plan estructurado** que detalle:
  1. Lista exacta de archivos a crear, modificar o eliminar.
  2. Decisiones técnicas y justificación de enfoque.
  3. Evaluación explícita de los **6 atributos de calidad**:
     - **Funcionalidad**: ¿Cumple exactamente el requerimiento sin excesos ni omisiones?
     - **Mantenibilidad**: ¿Es modular, legible y respeta principios SOLID / DRY?
     - **Rendimiento**: ¿Evita cuellos de botella, fugas de memoria o bloqueos de hilo?
     - **Seguridad**: ¿Valida entradas, previene inyecciones y protege datos sensibles?
     - **Observabilidad**: ¿Emite logs estructurados y facilita diagnósticos de fallo?
     - **Usabilidad**: ¿La API o interfaz resulta intuitiva y predecible?
- **Esperar aprobación explícita**: No ejecutes herramientas de edición hasta que el desarrollador humano valide el plan.

### 3. Principio de Claridad: No supongas
- Si un requerimiento, contrato de datos, flujo de usuario o dependencia es ambiguo, **pregunta inmediatamente al desarrollador**.
- Está terminantemente prohibido asumir decisiones de negocio o arquitectónicas sin confirmación previa.

### 4. Control Estricto de Permisos y Mutación de Estado
- **Lectura libre**: Puedes inspeccionar archivos, listar directorios y ejecutar búsquedas sin pedir confirmación.
- **Edición y creación restringidas**: Todo cambio en el sistema de archivos (crear, modificar o eliminar archivos) debe ser propuesto detallando el contenido exacto y requerir confirmación previa.
- **Comandos de Git que mutan estado**: Cualquier comando que altere el historial o las referencias del repositorio (`commit`, `branch`, `checkout -b`, `merge`, `tag`, `push`, `rebase`, `reset`) requiere:
  1. Mostrar el comando exacto a ejecutar.
  2. Explicar brevemente su impacto.
  3. Esperar autorización explícita del desarrollador.

---

## 🌿 Flujo de Trabajo en Git y Estándar de Commits

### Modelo de Ramas
- `main`: Rama de producción. Solo contiene versiones estables y probadas, identificadas con etiquetas semánticas (`vX.Y.Z`). Protegida contra commits directos.
- `develop`: Rama de integración continua. Toda nueva funcionalidad converge aquí.
- **Ramas de trabajo temporales**:
  - `feature/<nombre-descriptivo>`: Nuevas capacidades o módulos.
  - `fix/<nombre-descriptivo>`: Corrección de errores.
  - `docs/<nombre-descriptivo>`: Actualización de documentación y especificaciones.
- **Integración**: Siempre fusionar ramas de trabajo hacia `develop` utilizando `--no-ff` (no fast-forward) para mantener la trazabilidad histórica de los merges.

### Convención de Commits y Autoría
- Seguir el estándar **Conventional Commits**:
  - `feat: <descripción concisa>`
  - `fix: <descripción concisa>`
  - `docs: <descripción concisa>`
  - `refactor: <descripción concisa>`
  - `test: <descripción concisa>`
  - `chore: <descripción concisa>`
- **Autoría 100% Humana**: Queda **estrictamente prohibido** agregar menciones como `Co-Authored-By: Claude`, `Generated by AI` o firmas de asistentes virtuales en los mensajes de commit. El repositorio refleja la autoría y responsabilidad del desarrollador humano.

---

## 🤖 Jerarquía: Agente Orquestador y Subagentes

Para optimizar consumo de contexto y garantizar calidad técnica:

1. **Agente Orquestador (Modelo Superior)**:
   - Mantiene la visión holística del proyecto.
   - Dialoga con el desarrollador humano.
   - Elabora planes de trabajo, evalúa atributos de calidad y revisa el resultado de los subagentes.
   - Nunca delega la toma de decisiones críticas.

2. **Subagentes (Modelos de Ejecución: Sonnet / Haiku / Flash)**:
   - Se instancian con alcances quirúrgicos y bien delimitados.
   - **Regla inquebrantable**: Los subagentes **NUNCA** interactúan directamente con el usuario ni le formulan preguntas; reportan exclusivamente al orquestador.
   - **Un solo escritor a la vez**: Queda prohibida la edición concurrente de archivos por múltiples agentes. Las tareas de escritura deben ser estrictamente secuenciales para prevenir condiciones de carrera y desincronizaciones de estado.

---

## 🧩 Integración con Gentle AI

El sistema se apoya en el conjunto de herramientas de Gentle AI bajo una jerarquía clara:

- **ODD (Opportunity-Driven Development)**:
  - Todo cambio funcional se articula a través de especificaciones en `odd/tasks/<nombre-tarea>.md`.
  - Cada tarea define su alcance, checklist de progreso y pruebas automatizadas (TDD) previas a la implementación.
- **RDD (Review-Driven Development)**:
  - Antes de proponer un commit o merge, se ejecuta la revisión mediante `gentle-ai review assess`.
  - El orquestador evalúa los hallazgos y resuelve cualquier objeción de calidad antes de someter la propuesta al desarrollador.
- **Engram**:
  - Empleado para almacenar decisiones arquitectónicas y aprendizajes acumulados entre sesiones de desarrollo.
- **Skill Registry (`.atl/skill-registry.md`)**:
  - Catálogo formal de habilidades reutilizables.
  - Al encomendar trabajo a un subagente, el orquestador debe declarar el bloque `## Skills to load before work` con las dependencias pertinentes.
- **CodeGraph**:
  - En repositorios con índice generado, el agente debe utilizar `codegraph_explore` y `codegraph_context` antes de realizar lecturas ciegas de archivos en disco.
- **Prevalencia Normativa**:
  - **`AGENTS.md` prevalece siempre**: En caso de conflicto entre directrices predeterminadas de Gentle AI y las reglas estipuladas en este documento, las órdenes de `AGENTS.md` tienen prioridad absoluta.
