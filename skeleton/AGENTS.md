# Reglas del Proyecto — {{NOMBRE_PROYECTO}}

> Este archivo contiene las instrucciones maestras y no negociables para cualquier agente de IA o desarrollador que trabaje en este repositorio.  
> Su cumplimiento es estricto y prevalece sobre cualquier convención genérica o heurística externa.

---

## Qué es el proyecto

{{NOMBRE_PROYECTO}} — {{DESCRIPCION_CORTA}}

### Árbol del Repositorio

```text
├── AGENTS.md                  # Este documento: reglas maestras, flujo y directrices obligatorias
├── CLAUDE.md                  # Reglas específicas para el uso con Claude Code / Gentle AI
├── odd/                       # Tareas y seguimiento guiado por operaciones (ODD)
│   └── tasks/                 # Hojas de tareas activas y completadas (_TEMPLATE-task.md)
├── docs/                      # Fuente única de verdad técnica, funcional y de planificación
│   ├── producto/              # Visión, requisitos funcionales (RF) y no funcionales (RNF)
│   ├── arquitectura/          # Overview del sistema, diagramas y decisiones (ADRs)
│   ├── plan/                  # Roadmap general y detalle de fases
│   └── guias/                 # Configuración de entorno, comandos de compilación y pruebas
├── design/                    # Referencias de UI/UX, tokens y DESIGN.md
│   ├── DESIGN.md              # Sistema de diseño, paleta, tipografía y reglas visuales
│   └── screens/               # Mockups y capturas de referencia visual
└── {{CARPETA_CODIGO}}/        # Código fuente de la aplicación
```

---

## Qué leer según la tarea

Antes de iniciar cualquier acción, consulta exclusivamente la documentación correspondiente para no asumir comportamientos:

| Tipo de tarea | Qué leer obligatoriamente |
| :--- | :--- |
| **Nueva funcionalidad o cambio de lógica** | `docs/producto/requisitos.md` y la fase activa en `docs/plan/roadmap.md` |
| **Diseño visual, componentes o estilos** | `design/DESIGN.md` y `.claude/skills/project-ui/SKILL.md` |
| **Arquitectura, estado o nuevas dependencias** | `docs/arquitectura/overview.md` y `docs/arquitectura/decisiones/` |
| **Comandos de test, linter, build o entorno** | `docs/guias/desarrollo.md` |
| **Consulta general o visión del producto** | `docs/README.md` y `docs/producto/vision.md` |

---

## Reglas principales (obligatorias)

1. **La documentación manda (`docs/`):**  
   Toda funcionalidad, comportamiento, flujo o texto proviene exclusivamente de `docs/`. Si algo no está documentado en `docs/producto/requisitos.md`, **no existe y no se implementa**. Ante cualquier duda, vacante o ambigüedad, no asumas: pregunta al usuario. Las capturas o imágenes en `design/` sirven únicamente de referencia estética; nunca introducen funciones, botones ni textos que no figuren en `docs/`.
2. **Lo visual se rige por `design/DESIGN.md`:**  
   Todo desarrollo visual debe acatar `design/DESIGN.md`. La sección inicial **"Notas del proyecto"** en `DESIGN.md` prevalece sobre el resto del documento y define reglas específicas de diseño.
3. **Prevalencia funcional:**  
   Si existiera alguna discrepancia funcional o conceptual entre `docs/` y `design/`, **prevalece siempre `docs/`**.
4. **Reglas transversales de plataforma:**  
   {{REGLAS_DE_PLATAFORMA}}
5. **Trabajo estricto por fases (`docs/plan/roadmap.md`):**  
   Se trabaja únicamente en la fase actualmente abierta. Queda estrictamente prohibido implementar pantallas, servicios o modelos destinados a fases posteriores.
6. **Plan antes que código:**  
   Antes de escribir o editar una sola línea de código, presenta siempre un plan conciso indicando: archivos a modificar o crear, paquetes requeridos y decisiones clave. Espera la aprobación explícita del usuario antes de proceder.
7. **No supongas:**  
   Si una instrucción es ambigua, incompleta o entra en conflicto con las especificaciones existentes, detén la ejecución y solicita aclaración.
8. **Análisis de Requisitos de Calidad:**  
   En cada planificación y entrega, evalúa brevemente los siguientes 6 pilares de calidad, adoptando siempre la solución estándar de menor coste y complejidad:
   - **Usabilidad:** Interfaz intuitiva, respuesta háptica/visual inmediata, estados vacíos/error claros.
   - **Seguridad y Privacidad:** Principio de mínimo privilegio, almacenamiento seguro, respeto absoluto de directrices offline si aplica.
   - **Rendimiento y Eficiencia:** Bajo consumo de CPU/memoria, evitar renders innecesarios, paginación o lazy-loading cuando aplique.
   - **Fiabilidad:** Tolerancia a fallos, manejo exhaustivo de excepciones y validaciones de bordes.
   - **Testeabilidad:** Código modular, inversión de dependencias y cobertura mediante tests unitarios y de integración.
   - **Accesibilidad:** Contrastes legibles, etiquetas semánticas y zonas de toque ergonómicas (mínimo 48x48dp).

---

## Permisos de lectura, modificación y borrado

- **Lectura:** El agente tiene permiso permanente para inspeccionar y leer cualquier archivo dentro del repositorio.
- **Modificación y creación:** Cualquier cambio, creación de archivo o ejecución de comando que altere el estado requiere **permiso explícito previo del usuario**.
- **Borrado:** Queda estrictamente prohibido eliminar archivos, carpetas o ramas sin una confirmación previa inequívoca del usuario.

---

## Flujo de trabajo (11 pasos)

Todo ciclo de desarrollo debe seguir secuencialmente estos 11 pasos:

1. **Propuesta de tarea:** Se define el objetivo de la feature o corrección.
2. **Comprobación en `docs/`:** Validar que la tarea pertenece a la fase activa en `docs/plan/roadmap.md` y cumple los requisitos de `docs/producto/requisitos.md`.
3. **Presentación del plan:** El agente presenta un plan detallado (archivos afectados, enfoque, pruebas a añadir) y **espera la aprobación del usuario**.
4. **Creación de rama Git:** Partiendo siempre desde `develop`:
   ```bash
   git checkout develop
   git pull
   git checkout -b feature/<nombre-descriptivo>
   ```
5. **Creación de hoja ODD:** Crear el archivo `odd/tasks/<feature>.md` clonando `odd/tasks/_TEMPLATE-task.md` con las subtareas y rutas de delegación.
6. **Implementación TDD y verificación continua:**
   - Escribir tests que fallen primero (**RED**).
   - Implementar el código necesario para pasarlos (**GREEN**).
   - Refactorizar manteniendo tests y linter en verde (**REFACTOR**).
   - Ejecutar linter y suites de pruebas automatizadas según `docs/guias/desarrollo.md`.
7. **Propuesta de commits:** Presentar al usuario los comandos exactos de commit bajo *Conventional Commits* para su aprobación (sin auto-commits).
8. **Prueba y validación del usuario:** El usuario prueba el cambio en su entorno o dispositivo físico.
9. **Entrega y reporte:** El agente genera el reporte final de calidad y verificación.
10. **Merge a `develop` y sincronización documental:**
    - Merge hacia `develop`.
    - Actualizar estado en `docs/plan/roadmap.md`.
    - Registrar cambios en `CHANGELOG.md` y documentar nuevos ADRs en `docs/arquitectura/decisiones/` si hubo elecciones estructurales.
11. **Cierre de versión / Release (si aplica):** Al completar una fase o release, merge de `develop` a `main`, creación del tag `vX.Y.Z` y preparación de la siguiente fase.

---

## Ramas (Git) y Git y borrados (obligatorio)

- **Estructura de ramas:**
  - `main`: Código de producción, estable y versionado con tags (`vX.Y.Z`).
  - `develop`: Rama integradora de desarrollo activo.
  - `feature/<nombre>`: Nuevas funcionalidades basadas en la fase actual.
  - `fix/<nombre>`: Corrección de errores.
- **Formato de mensajes de commit:** Se utiliza la especificación estricta de *Conventional Commits*:
  - `feat: <descripción concisa en imperativo>`
  - `fix: <descripción concisa>`
  - `docs: <cambios exclusivamente en documentación>`
  - `test: <adición o refactorización de pruebas>`
  - `refactor: <cambios de código sin modificar funcionalidad>`
  - `chore: <mantenimiento o configuración>`
- **Prohibiciones estrictas en Git:**
  - **Prohibido realizar commits automáticos:** El agente propone el comando completo y el usuario autoriza su ejecución.
  - **Prohibido incluir líneas `Co-Authored-By`**, menciones a modelos de lenguaje o atribuciones de autoría de IA en mensajes de commit o descripciones.

---

## Agentes y subagentes

- **Rol del Agente Principal:** Entiende el contexto global, planifica, toma decisiones de alto nivel, interactúa con el usuario, revisa la calidad del código y sintetiza los resultados.
- **Delegación a Subagentes:** Tareas mecánicas, generación de tests repetitivos, búsquedas de patrones o refactorizaciones aisladas pueden delegarse en modelos más ligeros y económicos (Sonnet, Haiku o Flash).
- **Reglas para Subagentes:**
  - Los subagentes **NUNCA** interactúan directamente con el usuario ni le formulan preguntas; reportan exclusivamente al agente principal.
  - Debe mantenerse siempre la regla de **un único escritor a la vez** para prevenir condiciones de carrera y sobrescritura de código.

---

## Gentle AI (obligatorio)

`AGENTS.md` prevalece siempre sobre las directrices genéricas del framework Gentle AI. La integración se rige por las siguientes herramientas:

| Módulo / Herramienta | Rol y Comportamiento Esperado |
| :--- | :--- |
| **ODD (Operation-Driven Development)** | Seguimiento de tareas en `odd/tasks/<feature>.md`. Los cambios de estado no generan auto-commits. |
| **RDD (Review-Driven Development)** | Ejecución de `gentle-ai review assess` sobre los cambios del working tree en cuanto se terminan de escribir, sin esperar a realizar commits. |
| **Engram** | Memoria semántica persistente (`mem_save`, `mem_search`) para retener decisiones técnicas e incidencias entre sesiones. |
| **Skill Registry** | Registro centralizado en `.atl/skill-registry.md` para skills locales del proyecto. |
| **CodeGraph** | Índice estructural en `.codegraph/`. Consultar antes de realizar lecturas masivas de archivos. |

---

## Documentación: Dónde va cada cosa ("Un dato vive en un solo sitio")

Para prevenir duplicidades y desincronizaciones:

- **Propósito, propuesta de valor y usuario:** `docs/producto/vision.md`
- **Funcionalidades, reglas de negocio y restricciones:** `docs/producto/requisitos.md`
- **Arquitectura global, capas y flujo de datos:** `docs/arquitectura/overview.md`
- **Decisiones arquitectónicas significativas:** `docs/arquitectura/decisiones/NNNN-*.md`
- **Hitos temporales y estado de fases:** `docs/plan/roadmap.md`
- **Tareas detalladas de la fase en curso:** `docs/plan/fases/fase-NN-*.md`
- **Configuración local, comandos y testing:** `docs/guias/desarrollo.md`
- **Guía de estilos, tokens y componentes visuales:** `design/DESIGN.md`

---

## Entorno del desarrollador

{{ENTORNO_DESARROLLADOR}}
