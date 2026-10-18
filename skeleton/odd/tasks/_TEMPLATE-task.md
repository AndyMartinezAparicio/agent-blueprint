# Tarea ODD: {{ID_TAREA}} — {{NOMBRE_FEATURE}}

---

## Metadatos de la Tarea

- **Objetivo:** {{OBJETIVO_DESCRIPTIVO}}
- **Rama Git:** `feature/{{NOMBRE_RAMA}}` (o `fix/{{NOMBRE_RAMA}}`)
- **Fase del Roadmap:** Fase {{NUMERO_FASE}} — {{NOMBRE_FASE}}
- **Requisitos Vinculados:** `RF-{{XX}}`, `RNF-{{YY}}` (según `docs/producto/requisitos.md`)
- **ADRs Relacionados:** `docs/arquitectura/decisiones/{{NUMERO_ADR}}-*.md` (o `N/A`)
- **Estado Global:** `[ ] En progreso` / `[ ] Completada` / `[ ] En revisión`

---

## Desglose de Subtareas

Cada subtarea indica su ruta de ejecución:
- `Route: parent + user` (decisiones de arquitectura, aprobación de planes, revisión final).
- `Route: delegated (Sonnet)` (implementación de lógica, TDD, refactorización con contexto guiado).
- `Route: delegated (Haiku)` (pruebas repetitivas, extracción de constantes, generación de mocks).

| ID | Subtarea | Ruta de Delegación | Archivos Afectados | Estado |
| :--- | :--- | :--- | :--- | :---: |
| **T0** | Verificación de especificaciones en `docs/` y diseño de plan | `parent + user` | `docs/producto/requisitos.md`, `odd/tasks/` | [ ] |
| **T1** | Escritura de pruebas automatizadas fallidas (TDD RED) | `delegated (Sonnet)` | `test/...` | [ ] |
| **T2** | Implementación del modelo y lógica de negocio (TDD GREEN) | `delegated (Sonnet)` | `lib/...`, `src/...` | [ ] |
| **T3** | Implementación / adaptación de UI y enlace con tokens de diseño | `delegated (Sonnet)` | `lib/ui/...`, `design/DESIGN.md` | [ ] |
| **T4** | Ejecución de linter, formateo y refactorización limpia | `delegated (Haiku)` | Todo el changeset | [ ] |
| **T5** | Revisión con Gentle AI (`gentle-ai review assess` sobre el working tree al terminar cambios, antes de proponer commits) | `parent + user` | Árbol de trabajo (*working tree*) | [ ] |
| **T6** | Propuesta de commits al usuario (comitear cambios ya revisados no dispara otra revisión) y validación en entorno real | `parent + user` | Git log / working tree | [ ] |

---

## Verificación Obligatoria de Calidad

Antes de presentar la tarea al usuario como finalizada, deben cumplirse todos los siguientes criterios:

- [ ] **Linter sin advertencias:** Ejecutar el linter del proyecto y verificar cero errores.
- [ ] **Tests Unitarios y de Integración en verde:** Todas las pruebas pasan exitosamente.
- [ ] **Cero strings quemados:** Todos los textos visibles utilizan el sistema de internacionalización.
- [ ] **Cero colores hardcodeados:** Se emplean exclusivamente los tokens de `design/DESIGN.md`.
- [ ] **Revisión RDD:** Evaluación con `gentle-ai review assess` superada sobre los cambios del árbol de trabajo en cuanto se terminan de escribir (antes de proponer commits; comitear cambios ya revisados no dispara otra revisión).

---

## Registro de Ejecución y Evidencias

### 1. Ciclo TDD
- **RED:** *Describir qué test falló inicialmente y con qué error.*
- **GREEN:** *Describir la implementación mínima que hizo pasar la prueba.*
- **REFACTOR:** *Describir las mejoras de estructura sin romper tests.*

### 2. Resultados de Pruebas y Linter
```text
[Pegar salida del comando de linter / tests según docs/guias/desarrollo.md]
```

### 3. Evaluaciones de Gentle AI Review
*(La revisión con `gentle-ai review assess` se evalúa sobre el árbol de trabajo al terminar los cambios, antes de proponer commits. Hacer commit de cambios ya revisados no dispara otra revisión).*
- **ID de Evaluación:** `REV-{{ID}}`
- **Resultado:** Aprobado / Sin observaciones críticas pendientes.

### 4. Commits Aprobados
*(Los commits se proponen al usuario antes de ejecutarse; los cambios ya revisados en el árbol de trabajo no se vuelven a revisar. Registrar aquí los hashes finales una vez confirmados).*
- `feat(modulo): {{descripcion del commit}}` — `hash: {{HASH}}`
