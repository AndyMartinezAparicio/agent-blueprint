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
│   ├── plan/                  # Roadmap, detalle de fases y pruebas pendientes en dispositivo (pruebas-pendientes.md)
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
   Al valorar o planificar cada función, y al entregarla, incluye un análisis breve de los atributos de calidad que apliquen. En cada problema que detectes, indica la solución estándar y probada de la plataforma y su coste. Son recomendaciones: se aplican solo con la aprobación del usuario.
   - **Usabilidad:** Interfaz intuitiva, respuesta háptica/visual inmediata, estados vacíos/error claros.
   - **Seguridad y Privacidad:** Principio de mínimo privilegio, almacenamiento seguro, respeto absoluto de directrices offline si aplica.
   - **Rendimiento y Eficiencia:** Bajo consumo de CPU/memoria, evitar renders innecesarios, paginación o lazy-loading cuando aplique.
   - **Fiabilidad:** Tolerancia a fallos, manejo exhaustivo de excepciones y validaciones de bordes.
   - **Testeabilidad:** Código modular, inversión de dependencias y cobertura mediante tests unitarios y de integración.
   - **Accesibilidad:** Contrastes legibles, etiquetas semánticas y zonas de toque ergonómicas (mínimo 48x48dp).
9. **Decisiones de diseño: skills primero.**  
   En toda decisión de diseño o visual (jerarquía, tarjeta o texto, componentes, tipografía, color, espaciado, estados), el agente carga y revisa antes las skills de diseño (`project-ui`, `material-design` y, según el caso, las skills de layout del stack como `flutter-build-responsive-layout` o `flutter-fix-layout-issues`), basa la propuesta en ellas e indica qué skill respalda cada opción. Al delegar trabajo de UI en subagentes, les pasa las rutas de esas skills.

---

## Permisos de lectura, edición, git y borrado

- **Lectura y edición:** El agente puede leer y editar archivos del repositorio sin pedir permiso, siempre dentro de una tarea con plan aprobado ([regla 6](#reglas-principales-obligatorias)).
- **Git:** Cualquier operación que cambie el estado del repositorio (commit, branch, switch, merge, rebase, reset, stash, tag, push, pull) se propone con los comandos exactos y se ejecuta solo tras la aprobación del usuario. Única excepción: los commits de módulos de una tarea con plan aprobado, en su rama de trabajo ([paso 7](#flujo-de-trabajo-11-pasos)). Los comandos de solo lectura (`status`, `log`, `diff`, `show`) no requieren aprobación.
- **Borrado:** Cualquier borrado (archivos, carpetas, ramas, datos) requiere la aprobación previa e inequívoca del usuario.
- **Compilar, ejecutar o instalar la aplicación:** el agente no lo hace sin permiso del usuario, que compila él mismo; si hay un motivo importante para hacerlo, lo explica y pide permiso.

---

## Flujo de trabajo (11 pasos)

Todo ciclo de desarrollo debe seguir secuencialmente estos 11 pasos:

1. **Propuesta de tarea:** Se define el objetivo de la feature o corrección.
2. **Comprobación en `docs/`:** Validar que la tarea pertenece a la fase activa en `docs/plan/roadmap.md` y cumple los requisitos de `docs/producto/requisitos.md`. Si no está documentada, primero se documenta, con aprobación del usuario.
3. **Presentación del plan:** El agente presenta un plan detallado (archivos afectados, paquetes, enfoque, pruebas a añadir, riesgos de la plataforma y requisitos de calidad) y **espera la aprobación del usuario**. **Prototipo primero en experiencia de uso dudosa:** si la tarea es una decisión de uso o de aspecto que no está clara (un gesto nuevo, un anuncio dentro de un flujo, un panel nuevo), el plan empieza por un prototipo mínimo, sin tests ni docs, para que el usuario lo pruebe. Solo si le convence se implementa completo; si no, se descarta sin coste.
4. **Creación de rama Git:** Partiendo siempre desde `develop` (con aprobación, según las reglas de Git):
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
   - Mientras se trabaja, ejecutar solo el linter y los tests del módulo; la suite completa se ejecuta **una vez antes de cada commit**, no tras cada cambio (comandos en `docs/guias/desarrollo.md`).
   - **El agente no compila, ejecuta ni instala la aplicación** sin permiso del usuario, que compila él mismo.
7. **Commits por módulo sin pedir aprobación en la rama de trabajo:** aprobar el plan de una tarea autoriza los commits de sus módulos en su rama `feature/*`, `fix/*` o `docs/*`, en formato *Conventional Commits*. Cada módulo revisado se comitea antes de preparar el siguiente, para que no se revise dos veces. El agente informa del hash de cada commit. Push, merge, tags, ramas y cualquier commit en `develop` o `main` siempre requieren aprobación.
8. **Pruebas en dispositivo sin parar el desarrollo:** el agente apunta en `docs/plan/pruebas-pendientes.md` cada prueba que el usuario tiene que hacer en su dispositivo (pasos y resultado esperado) y sigue con la siguiente tarea. El usuario las hace todas juntas cuando tiene tiempo; un fallo se convierte en una tarea nueva. **Excepción, riesgo alto:** las pruebas de las funciones de riesgo alto del perfil (por ejemplo gestos, borrado, compras o anuncios) se piden en cuanto se termina su tarea, sin bloquear la siguiente, no al cerrar la fase.
9. **Entrega y reporte:** resumen de lo hecho, pruebas apuntadas en las pruebas pendientes, criterios de aceptación de la fase marcados y reporte final de calidad y verificación.
10. **Merge a `develop` y sincronización documental (con aprobación del usuario):**
    - Merge hacia `develop` con `--no-ff`.
    - Actualizar estado en `docs/plan/roadmap.md`.
    - Registrar cambios en `docs/CHANGELOG.md` y documentar nuevos ADRs en `docs/arquitectura/decisiones/` si hubo elecciones estructurales.
11. **Cada fase aprobada se publica en `main`** cuando sus pruebas pendientes están en verde: avanzar `main` hasta `develop` (*fast-forward*) y crear el tag `vX.Y.Z` de la versión de la fase (comandos propuestos al usuario, como cualquier operación de git). Ninguna versión aprobada se queda solo en `develop`.

---

## Ramas (Git) y Git y borrados (obligatorio)

- **Estructura de ramas:**
  - `main`: Código de producción, estable y versionado con tags (`vX.Y.Z`).
  - `develop`: Rama integradora de desarrollo activo.
  - `feature/<nombre>`, `fix/<nombre>`, `docs/<nombre>`: Salen de `develop` y vuelven con merge `--no-ff`.
  - `hotfix/<nombre>`: Sale de `main` y se fusiona en `main` y `develop`.
  - Las ramas fusionadas se borran, con aprobación. **Nunca se trabaja directamente en `main` ni en `develop`.**
- **Formato de mensajes de commit:** Se utiliza la especificación estricta de *Conventional Commits*:
  - `feat: <descripción concisa en imperativo>`
  - `fix: <descripción concisa>`
  - `docs: <cambios exclusivamente en documentación>`
  - `test: <adición o refactorización de pruebas>`
  - `refactor: <cambios de código sin modificar funcionalidad>`
  - `chore: <mantenimiento o configuración>`
- **Aprobación:** las operaciones de git se rigen por la sección [Permisos](#permisos-de-lectura-edición-git-y-borrado): solo los commits de módulos en la rama de trabajo de una tarea con plan aprobado se hacen sin pedir permiso.
- **Prohibiciones estrictas en Git:**
  - **Prohibido incluir líneas `Co-Authored-By`**, menciones a modelos de lenguaje o atribuciones de autoría de IA en mensajes de commit o descripciones.

---

## Agentes y subagentes

- **Rol del Agente Principal:** Entiende el contexto global, planifica, toma decisiones de alto nivel, interactúa con el usuario, revisa la calidad del código y sintetiza los resultados.
- **Delegación solo cuando compensa:** cada subagente gasta unos 100.000 tokens leyendo contexto antes de escribir. Umbral:
  - **Cambios de menos de unas 30 líneas** (corregir un test, una frase, un import, aplicar un aviso de revisión), git de estado y consultas: los hace el agente principal directamente.
  - **Trabajo mediano o grande** (un módulo con su código, tests y docs): **Sonnet**.
  - **Solo documentación mecánica** o búsquedas simples: **Haiku**.
- Las tareas de documentación de una tarea se agrupan en un solo encargo, no uno por archivo.
- **Reglas para Subagentes:**
  - Los subagentes **NUNCA** interactúan directamente con el usuario ni le formulan preguntas; la aprobación la pide el agente principal antes de delegar.
  - El agente principal revisa siempre lo que entrega un subagente.
  - Debe mantenerse siempre la regla de **un único escritor a la vez** para prevenir condiciones de carrera y sobrescritura de código.

---

## Gentle AI (obligatorio)

Este entorno usa **Gentle AI** (gentle-ai 4.2.0) como capa de configuración de agentes. Cualquier agente que trabaje aquí debe respetar sus convenciones.

**Prioridad: este AGENTS.md va por encima de Gentle AI.** Si una regla de Gentle AI (incluidas las que inyecta en `~/.claude/CLAUDE.md` o cambian al actualizarlo) contradice este archivo, se sigue este archivo y el agente avisa del conflicto al usuario. En particular, el uso de subagentes de la sección [Agentes y subagentes](#agentes-y-subagentes) y la aprobación de git y borrados prevalecen sobre el "trabajo en línea por defecto" de Gentle AI. Lo que este archivo no regula sigue las convenciones de Gentle AI.

| Componente | Qué es | Qué exige |
|---|---|---|
| **ODD** (Organic Driven Development) | Flujo por defecto | El trabajo sustancial se registra en `odd/tasks/<feature>.md` (con espejo en Engram, topic `odd/<feature>/tasks`) antes de la primera escritura. Cada tarea se marca solo con evidencia. Las tareas pequeñas no crean documento. **En este proyecto** los commits por módulo se hacen sin pedir aprobación solo en la rama de trabajo de una tarea con plan aprobado ([paso 7](#flujo-de-trabajo-11-pasos)). |
| **RDD** (receipt-driven development / revisión nativa) | `gentle-ai review` | Activado globalmente. Cada candidato de riesgo medio o alto pide consentimiento al usuario (revisar o saltar). **Regla del proyecto: revisión modular al implementar.** Cada módulo pequeño (un archivo o un grupo de archivos de una misma pieza: un componente con su test, un controlador, los textos de una pantalla) se revisa en cuanto se termina de implementar, antes del siguiente módulo y sin esperar al commit: se preparan solo sus archivos con `git add <archivos>` y se evalúa y revisa con `--projection staged` (`gentle-ai review assess` y `gentle-ai review status ... --projection staged`). Nunca se acumula un cambio grande para revisarlo de golpe. Cada módulo revisado se comitea antes de preparar el siguiente: si se queda preparado, la revisión siguiente lo vuelve a incluir. **Hacer commit no dispara revisión:** los módulos ya revisados se comitean sin revisarse otra vez; la regla de Gentle AI de revisar tras cada commit (`--committed-only`) no se aplica en este proyecto, y el aviso automático de Gentle AI al terminar cada respuesta (`gentle-ai review stop-hook`) está desactivado para este proyecto con el archivo `.claude/gentle-ai-stop-hook.off`. Si un commit incluye cambios que no se revisaron, esos se revisan por módulos antes de comitear. Nunca se elude ni se responde por el usuario. El usuario lo controla con `gentle-ai review mode status\|enable\|disable`. |
| **Engram** | Memoria persistente entre sesiones | Guarda decisiones, descubrimientos y resúmenes de sesión. |
| **Skill registry** | `.atl/skill-registry.md`, índice de skills | Se regenera con `gentle-ai skill-registry refresh`. El agente principal pasa las rutas de skills a los subagentes. La caché `.atl/.skill-registry.cache.json` no se versiona. |
| **CodeGraph** | Índice de código en `.codegraph/` (local, ignorado por git) | Usarlo antes de búsquedas amplias en el código. |

Las skills del proyecto viven en `.claude/skills/`: las propias `project-ui` y `material-design` (guía Material 3 destilada de fuentes oficiales), junto a las skills de apoyo del stack. Tras añadir o cambiar skills, ejecuta `gentle-ai skill-registry refresh`. Las skills de terceros se revisan antes de instalarlas. Gentle AI añade `.atl/` al `.gitignore` en cada refresco: `.atl/skill-registry.md` sigue versionado y sus cambios se suben con `git add -u .atl`. Sus rutas son absolutas de esta máquina; en otro equipo se regenera con `gentle-ai skill-registry refresh`.

Los agentes que no soporten las herramientas de Gentle AI deben seguir al menos las convenciones escritas: archivos `odd/tasks/`, aprobación de git y revisión sin eludir.

---

## Documentación: Dónde va cada cosa ("Un dato vive en un solo sitio")

Para prevenir duplicidades y desincronizaciones. El detalle de una función (comportamiento, textos, casos) se escribe solo en los requisitos (`RF-n`). El plan de la fase, `design/DESIGN.md`, la visión, el CHANGELOG y los ADR lo resumen en una línea y enlazan al RF, en lugar de repetirlo.

- **Propósito, propuesta de valor y usuario:** `docs/producto/vision.md`
- **Funcionalidades, reglas de negocio y restricciones:** `docs/producto/requisitos.md`
- **Arquitectura global, capas y flujo de datos:** `docs/arquitectura/overview.md`
- **Decisiones arquitectónicas significativas:** `docs/arquitectura/decisiones/NNNN-*.md` (los ADR aceptados no se reescriben: se crea uno nuevo que lo sustituye)
- **Hitos temporales y estado de fases:** `docs/plan/roadmap.md`
- **Tareas detalladas de la fase en curso:** `docs/plan/fases/fase-NN-*.md`
- **Pruebas que el usuario debe hacer en su dispositivo:** `docs/plan/pruebas-pendientes.md`
- **Tareas en curso (ODD):** `odd/tasks/<feature>.md`
- **Lo hecho:** `docs/CHANGELOG.md`
- **Configuración local, comandos y testing:** `docs/guias/desarrollo.md`
- **Guía de estilos, tokens y componentes visuales:** `design/DESIGN.md`

---

## Idioma

El agente responde siempre en español. El idioma de los artefactos técnicos (código, comentarios, mensajes de commit) sigue la convención del proyecto.

---

## Entorno del desarrollador

{{ENTORNO_DESARROLLADOR}}
