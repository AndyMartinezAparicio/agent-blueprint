@AGENTS.md

# Directrices Específicas para Claude Code

Este archivo complementa a [AGENTS.md](file:///C:/Users/Andy/Desktop/Proyectos%20extras/agent-blueprint/AGENTS.md) con instrucciones optimizadas para la ejecución de **Claude Code**.

---

## 🤖 Selección y Delegación de Modelos para Subagentes

Al invocar subagentes mediante la herramienta de subagentes en Claude Code, selecciona el modelo según la naturaleza de la tarea:

- **`model: "sonnet"`**:
  - Operaciones de Git (inspección de diffs, preparación de ramas y comandos estructurados).
  - Manipulación y escritura de código fuente y pruebas unitarias (TDD).
  - Diseño y aplicación de plantillas de arquitectura y refactorizaciones complejas.
  - Exploración técnica profunda y resolución de dependencias no triviales.

- **`model: "haiku"`**:
  - Redacción y formateo de documentación mecánica y tablas de estado.
  - Búsquedas simples de cadenas de texto y cotejo de nombres de archivo.
  - Verificación superficial de listas de verificación o sintaxis básica.

---

## 🧭 Integración de Herramientas de Contexto Avanzado

### 1. CodeGraph
- Si el repositorio cuenta con un índice generado (`.codegraph/`), invoca `codegraph_explore` y `codegraph_context` **antes** de realizar lecturas masivas o dispersas de archivos individuales.
- Utiliza la navegación por grafos para mapear llamadas de funciones, dependencias entre módulos y referencias de tipos.

### 2. Engram (Memoria Persistente)
- **Registro de decisiones**: Tras consensuar una decisión arquitectónica o una resolución de diseño importante con el usuario, persiste el contexto mediante `mem_save`.
- **Recuperación al inicio**: Al iniciar una sesión o una nueva fase, ejecuta `mem_search` para consultar precedentes, restricciones aprendidas en iteraciones previas o acuerdos vigentes.
- Guarda un resumen conciso de estado al concluir hitos relevantes.

---

## 🎨 Decisiones de Diseño y UI (Skills Primero)

- En decisiones de diseño o visuales, carga y revisa antes las skills de diseño (`project-ui`, `material-design` y, si aplica, las de layout como `flutter-build-responsive-layout` o `flutter-fix-layout-issues`), justifica cada opción con la skill que la respalda y pasa sus rutas a los subagentes de UI.

---

## 🔍 Ciclo de Revisiones Nativas (Gentle AI Review)

- Sigue las transiciones de `gentle-ai review` tal como las devuelve la herramienta.
- **Evaluación sobre el árbol de trabajo**: La revisión se evalúa y se propone sobre los cambios del árbol de trabajo en cuanto se terminan (`gentle-ai review assess` sobre los cambios actuales), sin esperar a que haya commits.
- **Hacer commit no dispara otra revisión**: Los cambios ya revisados en el árbol de trabajo se comitean sin revisarse otra vez; la regla de Gentle AI de revisar tras cada commit (`--committed-only`) no se aplica en este proyecto. Si el commit incluye cambios que no se revisaron, esos sí se revisan antes de comitear.
- **Punto de decisión humano**: Cada candidato de riesgo medio o alto pide consentimiento al usuario (revisar o saltar). Nunca se elude ni se responde por el usuario. El usuario lo controla con `gentle-ai review mode status|enable|disable`.
