# Directrices de Claude Code — Integración con AGENTS.md

@AGENTS.md

> Este archivo complementa `AGENTS.md` con instrucciones específicas y directivas operativas para el entorno **Claude Code** y herramientas del ecosistema Gentle AI.

---

## 1. Modelo de Ejecución y Delegación de Subagentes

- **Agente Principal:** Se ejecuta sobre el modelo superior (Opus / Sonnet 3.7 / según configuración de sesión) para comprender la intención del usuario, diseñar planes de implementación, formular preguntas aclaratorias y realizar revisiones de código de alto nivel.
- **Subagentes y Delegación:** delega solo cuando compensa, porque cada subagente gasta unos 100.000 tokens leyendo contexto antes de escribir ([umbral completo en `AGENTS.md`](AGENTS.md#agentes-y-subagentes)):
  - Cambios de menos de unas 30 líneas (corregir un test, una frase, un import, aplicar un aviso de revisión), git de estado y consultas: los hace el agente principal directamente.
  - Trabajo mediano o grande (un módulo con su código, tests y docs): invoca un subagente con `model: "sonnet"`.
  - Solo documentación mecánica o búsquedas simples: `model: "haiku"`.
  - Las tareas de documentación de una tarea se agrupan en un solo encargo, no uno por archivo.
  - **Regla estricta:** Ningún subagente debe interactuar directamente con el usuario ni pedir aprobaciones. La aprobación la pide el agente principal antes de delegar, y revisa siempre lo que el subagente entrega.
  - Solo un agente puede editar archivos a la vez para evitar colisiones en el árbol de trabajo.

---

## 2. Inspección Estructural con CodeGraph

- Antes de leer masivamente múltiples archivos del repositorio o buscar referencias a ciegas con `grep`/`find`, utiliza siempre la herramienta estructural de CodeGraph:
  - Invoca `codegraph_explore` para identificar símbolos, dependencias, jerarquías de clases y relaciones de llamadas.
  - Esto minimiza el consumo innecesario de contexto y garantiza una navegación precisa por el codebase.

---

## 3. Memoria Persistente con Engram

- Consulta y actualiza la memoria persistente del proyecto durante la sesión:
  - `mem_search`: Ejecútalo al inicio de tareas complejas para recuperar decisiones técnicas previas, advertencias de bugs resueltos o convenciones fijadas en sesiones anteriores.
  - `mem_save`: Úsalo tras resolver un problema complejo, acordar una solución de arquitectura no obvia con el usuario o identificar una particularidad crítica del entorno local.

---

## 4. Evaluaciones RDD con Gentle AI Review

- Sigue las transiciones de `gentle-ai review` tal como las devuelve la herramienta.
- **Revisión modular al implementar:** cada módulo pequeño (un archivo o un grupo de archivos de una misma pieza) se revisa en cuanto se termina, antes del siguiente módulo y sin esperar al commit. Prepara solo sus archivos y evalúa sobre lo preparado:
  ```bash
  git add <archivos>
  gentle-ai review assess --projection staged
  gentle-ai review status ... --projection staged
  ```
- Nunca acumules un cambio grande para revisarlo de golpe. Cada módulo revisado se comitea antes de preparar el siguiente: si se queda preparado, la revisión siguiente lo vuelve a incluir.
- **Hacer commit no dispara revisión:** los módulos ya revisados se comitean sin revisarse otra vez (la regla de `--committed-only` no se aplica en este proyecto). Si un commit incluye cambios que no se revisaron, esos se revisan por módulos antes de comitear.
- El aviso automático de Gentle AI al terminar cada respuesta (`gentle-ai review stop-hook`) está desactivado en este proyecto con el archivo `.claude/gentle-ai-stop-hook.off`.
- En candidatos de riesgo medio o alto, se pide consentimiento al usuario (revisar o saltar) sin eludirlo ni responder por él.
- Si el informe arroja advertencias de calidad o lints, corrígelos de inmediato antes de solicitar la revisión humana o proponer commits.

---

## 5. Recordatorios Operativos Fundamentales

1. **Permisos:** Puedes leer y editar archivos sin pedir permiso dentro de una tarea con plan aprobado. Requieren aprobación del usuario cualquier operación de git que cambie el estado (propón los comandos exactos) y cualquier borrado. No compiles, ejecutes ni instales la aplicación sin permiso.
2. **Commits:** Aprobar el plan de una tarea autoriza los commits de sus módulos, en formato *Conventional Commits*, en su rama `feature/*`, `fix/*` o `docs/*`; informa del hash de cada uno. Push, merge, tags, ramas y cualquier commit en `develop` o `main` siempre requieren aprobación.
3. **Flujo TDD:** Escribe primero la prueba que falle (RED), implementa el código mínimo para pasarla (GREEN) y refactoriza (REFACTOR). Mientras trabajas ejecuta solo los tests del módulo; la suite completa, una vez antes de cada commit.
4. **Cero atribuciones de IA en Git:** Prohibido incluir menciones como `Co-Authored-By` o notas automáticas de IA en commits o PRs.
5. **Decisiones de diseño (skills primero):** En decisiones de diseño o visuales, carga y revisa antes las skills de diseño (`project-ui`, `material-design` y, si aplica, `flutter-build-responsive-layout` o `flutter-fix-layout-issues`), justifica cada opción con la skill que la respalda y pasa sus rutas a los subagentes de UI.
