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
| **Diseño visual, componentes o estilos** | `design/DESIGN.md`, `.claude/skills/project-ui/SKILL.md` y `.claude/skills/material-design/SKILL.md` |
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
9. **Decisiones de diseño: skills primero.**  
   En toda decisión de diseño o visual (jerarquía, tarjeta o texto, componentes, tipografía, color, espaciado, estados), el agente carga y revisa antes las skills de diseño (`project-ui`, `material-design` y, según el caso, las skills de layout del stack como `flutter-build-responsive-layout` o `flutter-fix-layout-issues`), basa la propuesta en ellas e indica qué skill respalda cada opción. Al delegar trabajo de UI en subagentes, les pasa las rutas de esas skills.

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

Este entorno usa **Gentle AI** (gentle-ai 4.2.0) como capa de configuración de agentes. Cualquier agente que trabaje aquí debe respetar sus convenciones.

**Prioridad: este AGENTS.md va por encima de Gentle AI.** Si una regla de Gentle AI (incluidas las que inyecta en `~/.claude/CLAUDE.md` o cambian al actualizarlo) contradice este archivo, se sigue este archivo y el agente avisa del conflicto al usuario. En particular, el uso de subagentes de la sección [Agentes y subagentes](#agentes-y-subagentes) y la aprobación de git y borrados prevalecen sobre el "trabajo en línea por defecto" de Gentle AI. Lo que este archivo no regula sigue las convenciones de Gentle AI.

| Componente | Qué es | Qué exige |
|---|---|---|
| **ODD** (Organic Driven Development) | Flujo por defecto | El trabajo sustancial se registra en `odd/tasks/<feature>.md` (con espejo en Engram, topic `odd/<feature>/tasks`) antes de la primera escritura. Cada tarea se marca solo con evidencia. Las tareas pequeñas no crean documento. **Excepción de este proyecto:** los commits automáticos por tarea de ODD NO se hacen sin aprobación del usuario ([regla de Git](#git-y-borrados-obligatorio)). |
| **RDD** (receipt-driven development / revisión nativa) | `gentle-ai review` | Activado globalmente. Cada candidato de riesgo medio o alto pide consentimiento al usuario (revisar o saltar). **Regla del proyecto:** la revisión se evalúa y se propone sobre los cambios del árbol de trabajo en cuanto se terminan (`gentle-ai review assess` sobre los cambios actuales), sin esperar a que haya commits. **Hacer commit no dispara otra revisión:** los cambios ya revisados en el árbol de trabajo se comitean sin revisarse otra vez, y la regla de Gentle AI de revisar tras cada commit (`--committed-only`) no se aplica en este proyecto. Si el commit incluye cambios que no se revisaron, esos sí se revisan antes de comitear. Nunca se elude ni se responde por el usuario. El usuario lo controla con `gentle-ai review mode status\|enable\|disable`. |
| **Engram** | Memoria persistente entre sesiones | Guarda decisiones, descubrimientos y resúmenes de sesión. |
| **Skill registry** | `.atl/skill-registry.md`, índice de skills | Se regenera con `gentle-ai skill-registry refresh`. El agente principal pasa las rutas de skills a los subagentes. La caché `.atl/.skill-registry.cache.json` no se versiona. |
| **CodeGraph** | Índice de código en `.codegraph/` (local, ignorado por git) | Usarlo antes de búsquedas amplias en el código. |

Las skills del proyecto viven en `.claude/skills/`: las propias `project-ui` y `material-design` (guía Material 3 destilada de fuentes oficiales), junto a las skills de apoyo del stack. Tras añadir o cambiar skills, ejecuta `gentle-ai skill-registry refresh`. Las skills de terceros se revisan antes de instalarlas. Gentle AI añade `.atl/` al `.gitignore` en cada refresco: `.atl/skill-registry.md` sigue versionado y sus cambios se suben con `git add -u .atl`. Sus rutas son absolutas de esta máquina; en otro equipo se regenera con `gentle-ai skill-registry refresh`.

Los agentes que no soporten las herramientas de Gentle AI deben seguir al menos las convenciones escritas: archivos `odd/tasks/`, aprobación de git y revisión sin eludir.

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
