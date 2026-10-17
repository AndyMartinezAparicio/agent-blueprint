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

## 🔍 Ciclo de Revisiones Nativas (Gentle AI Review)

- Al realizar evaluaciones de calidad bajo el flujo de Review-Driven Development (RDD), respeta las transiciones formales de estado de `gentle-ai review`:
  1. **Planning**: Identificación de riesgos y checklist de verificación.
  2. **Assessment**: Evaluación de métricas y atributos con `gentle-ai review assess`.
  3. **Decision**: Consulta activa y validación con el usuario.
- **Punto de decisión humano**: Presenta siempre los hallazgos de forma clara y pide decisión explícita al desarrollador humano antes de cerrar una revisión o proceder con la fusión a ramas estables.
