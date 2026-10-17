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

- La revisión por Gentle AI (`gentle-ai review`) se ejecuta en modo continuo sobre los cambios del árbol de trabajo (*working tree*), **sin esperar a que se hagan commits**.
- Transiciones operativas:
  - Al completar la edición de un archivo o conjunto de cambios funcionales, ejecuta la evaluación de revisión:
    ```bash
    gentle-ai review assess
    ```
  - Si el informe arroja advertencias de calidad o lints, corrígelos de inmediato antes de solicitar la revisión humana.

---

## 5. Recordatorios Operativos Fundamentales

1. **Permiso previo obligatorio:** Cualquier creación, edición o borrado de archivos requiere autorización previa explícita del usuario.
2. **Prohibido el auto-commit:** Nunca ejecutes `git commit` directamente. Presenta siempre el comando exacto al usuario en formato *Conventional Commits* y espera su confirmación.
3. **Flujo TDD:** Escribe primero la prueba que falle (RED), implementa el código mínimo para pasarla (GREEN) y refactoriza (REFACTOR).
4. **Cero atribuciones de IA en Git:** Prohibido incluir menciones como `Co-Authored-By` o notas automáticas de IA en commits o PRs.
