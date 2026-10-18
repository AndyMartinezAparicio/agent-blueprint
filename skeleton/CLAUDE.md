# Directrices de Claude Code — Integración con AGENTS.md

@AGENTS.md

> Este archivo complementa `AGENTS.md` con instrucciones específicas y directivas operativas para el entorno **Claude Code** y herramientas del ecosistema Gentle AI.

---

## 1. Modelo de Ejecución y Delegación de Subagentes

- **Agente Principal:** Se ejecuta sobre el modelo superior (Opus / Sonnet 3.7 / según configuración de sesión) para comprender la intención del usuario, diseñar planes de implementación, formular preguntas aclaratorias y realizar revisiones de código de alto nivel.
- **Subagentes y Delegación:**
  - Para tareas mecánicas (escritura de tests unitarios a partir de especificaciones, refactorizaciones sintácticas repetitivas, generación de mocks o búsqueda de cadenas), invoca subagentes especificando explícitamente:
    - `model: "sonnet"` para tareas de implementación guiada o generación de código con contexto medio.
    - `model: "haiku"` para tareas de extracción rápida, formateo o comprobaciones de texto.
  - **Regla estricta:** Ningún subagente debe interactuar directamente con el usuario ni pedir aprobaciones. Toda síntesis y comunicación pasa a través del agente principal.
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
- La revisión (`gentle-ai review assess`) se evalúa sobre los cambios del árbol de trabajo (*working tree*) en cuanto se terminan, sin esperar a que haya commits:
  ```bash
  gentle-ai review assess
  ```
- **Hacer commit no dispara otra revisión:** los cambios ya revisados en el árbol de trabajo se comitean sin revisarse otra vez (la regla de `--committed-only` no se aplica en este proyecto). Si el commit incluye cambios que no se revisaron, esos sí se revisan antes de comitear.
- En candidatos de riesgo medio o alto, se pide consentimiento al usuario (revisar o saltar) sin eludirlo ni responder por él.
- Si el informe arroja advertencias de calidad o lints, corrígelos de inmediato antes de solicitar la revisión humana o proponer commits.

---

## 5. Recordatorios Operativos Fundamentales

1. **Permiso previo obligatorio:** Cualquier creación, edición o borrado de archivos requiere autorización previa explícita del usuario.
2. **Prohibido el auto-commit:** Nunca ejecutes `git commit` directamente. Presenta siempre el comando exacto al usuario en formato *Conventional Commits* y espera su confirmación.
3. **Flujo TDD:** Escribe primero la prueba que falle (RED), implementa el código mínimo para pasarla (GREEN) y refactoriza (REFACTOR).
4. **Cero atribuciones de IA en Git:** Prohibido incluir menciones como `Co-Authored-By` o notas automáticas de IA en commits o PRs.
5. **Decisiones de diseño (skills primero):** En decisiones de diseño o visuales, carga y revisa antes las skills de diseño (`project-ui`, `material-design` y, si aplica, `flutter-build-responsive-layout` o `flutter-fix-layout-issues`), justifica cada opción con la skill que la respalda y pasa sus rutas a los subagentes de UI.
