# Configurar un equipo nuevo para trabajar con agentes

Esta guía deja un ordenador nuevo listo para trabajar con proyectos creados desde Agent Blueprint (o con sus mismas reglas). Parte de un equipo sin configurar y termina con una lista de comprobación. Para crear un proyecto, ve a la [guía de creación de proyectos](crear-proyecto.md).

---

## 1. Prerrequisitos

Instala a mano, antes de pedir nada al agente:

- **Git**, accesible desde la línea de comandos (`git --version`).
- **Claude Code** (o el agente de IA que uses).
- **Gentle AI** (`gentle-ai --version`). **Engram** (memoria persistente) y **CodeGraph** (índice de código) vienen con Gentle AI: no se instalan por separado.

---

## 2. Lo que viaja con cada repositorio (no hay que hacer nada)

Un proyecto creado desde el esqueleto ya trae, versionado en su repositorio:

- `AGENTS.md` y `CLAUDE.md`: reglas del proyecto.
- `.claude/skills/`: skills del proyecto (`project-ui`, `material-design` y las de apoyo del stack).
- `.gitattributes`: finales de línea LF en todos los sistemas.
- `.claude/gentle-ai-stop-hook.off`: desactiva el aviso de revisión al final de cada respuesta en ese proyecto (la revisión se hace por módulos).

Esos archivos no se configuran en el equipo nuevo: basta con clonar el repositorio.

---

## 3. Qué pedir al agente tras instalar Gentle AI

Abre el agente en cualquier carpeta y pídele, en este orden:

1. **Estilo de respuesta:** poner el output style en `Neutral`.
2. **Reglas personales** en la sección `## Rules` de `~/.claude/CLAUDE.md`, por encima del bloque de Gentle AI: sin `Co-Authored-By` ni atribución de IA y con Conventional Commits; respuestas cortas; una sola pregunta cada vez; sin menús de opciones salvo elección real; verificar antes de dar la razón; responder siempre en español. El texto exacto está en el [bloque del apartado 4](#4-prompt-para-hacerlo-todo-de-una-vez).
3. **Aviso de revisión al final de cada respuesta:** en `~/.claude/settings.json`, envolver el hook `gentle-ai review stop-hook` para que salga sin hacer nada si existe `.claude/gentle-ai-stop-hook.off` en el proyecto:
   `if [ -f "${CLAUDE_PROJECT_DIR:-.}/.claude/gentle-ai-stop-hook.off" ]; then cat >/dev/null; exit 0; fi; exec gentle-ai review stop-hook --agent claude-code`.
4. **Por cada proyecto clonado:** `gentle-ai skill-registry refresh` (sus rutas son absolutas de cada equipo) y `gentle-ai codegraph init --cwd <proyecto>`.
5. **Revisión nativa:** comprobar `gentle-ai review mode status` (activada por defecto).
6. **Git global:** `user.name` y `user.email` iguales que en el otro equipo.
7. **Modo sin preguntas de permisos (bypass):** en `~/.claude/settings.json`, `"permissions": { "defaultMode": "bypassPermissions" }` y `"skipDangerousModePermissionPrompt": true`. El agente ya no pide permiso para cada comando o edición; los límites los ponen las reglas de `AGENTS.md` (aprobación de git y borrados, no compilar sin permiso).

> [!WARNING]
> Con el modo bypass, Claude Code no frena ningún comando: lo que impide un `git push`, un borrado o una compilación sin tu permiso son solo las reglas escritas. Úsalo solo en tu equipo personal y con proyectos que tengan esas reglas en su `AGENTS.md`.

> [!WARNING]
> `gentle-ai sync` y las actualizaciones de Gentle AI pueden reescribir el envoltorio del hook en `~/.claude/settings.json` y el contenido de `~/.claude/CLAUDE.md`. Tras actualizar, vuelve a comprobar los puntos 2, 3 y 7.

---

## 4. Prompt para hacerlo todo de una vez

Los puntos 1 a 7 se pueden pedir en un solo mensaje. Pega esto en el agente (sustituye `<RUTA_DEL_PROYECTO>` por cada repositorio clonado, o quita el punto 4 si aún no has clonado ninguno):

````text
Configura este equipo para trabajar con Gentle AI. Haz estos 7 puntos, uno tras otro, y al terminar dime qué cambiaste y qué quedó pendiente. No toques nada que no figure aquí.

1. Pon el output style en Neutral.

2. En ~/.claude/CLAUDE.md, añade (o reemplaza si ya existe) la sección "## Rules" por encima del bloque de Gentle AI, con exactamente este texto:

## Rules
- Never add "Co-Authored-By" or AI attribution to commits. Use conventional commits only.
- Response-length contract: default to short answers. Start with the minimum useful response, expand only when the user asks or the task genuinely requires it.
- Ask at most one question at a time. After asking it, STOP and wait.
- Do not present option menus, exhaustive lists, or multiple approaches unless there is a real fork with meaningful tradeoffs.
- If unsure about length or detail, choose the shorter response.
- When asking a question, STOP and wait for response. Never continue or assume answers.
- Never agree with user claims without verification. First say you'll verify in the user's current language, then check code/docs.
- If user is wrong, explain WHY with evidence. If you were wrong, acknowledge with proof.
- Always propose alternatives with tradeoffs when relevant.
- Verify technical claims before stating them. If unsure, investigate first.
- Always reply to the user in Spanish; never switch to English.

3. En ~/.claude/settings.json, envuelve el hook "gentle-ai review stop-hook" para que salga sin hacer nada si existe .claude/gentle-ai-stop-hook.off en el proyecto. El comando del hook pasa a ser:
   if [ -f "${CLAUDE_PROJECT_DIR:-.}/.claude/gentle-ai-stop-hook.off" ]; then cat >/dev/null; exit 0; fi; exec gentle-ai review stop-hook --agent claude-code

4. Para cada proyecto clonado (<RUTA_DEL_PROYECTO>): ejecuta "gentle-ai skill-registry refresh" y "gentle-ai codegraph init --cwd <RUTA_DEL_PROYECTO>".

5. Ejecuta "gentle-ai review mode status" y dime el resultado (debe estar activada). No la cambies.

6. Ejecuta "git config --global user.name" y "git config --global user.email" y dime los valores. Si faltan, pregúntame cuáles poner; no los inventes.

7. En ~/.claude/settings.json, pon "permissions": { "defaultMode": "bypassPermissions" } (conservando el resto de "permissions") y "skipDangerousModePermissionPrompt": true. El cambio se aplica al abrir una sesión nueva.
````

---

## 5. Qué copiar del equipo anterior

8. **Memoria de Claude Code:** la carpeta `~/.claude/projects/<proyecto>/memory/` de cada proyecto. El nombre de la carpeta `<proyecto>` depende de la ruta del proyecto en cada equipo, así que copia el contenido a la carpeta equivalente del equipo nuevo (ábrela una vez con el agente para que se cree).
9. **Memoria de Engram:** en el equipo viejo, `engram export engram-export.json --all`; copia el archivo al equipo nuevo y ejecuta `engram import engram-export.json`.

---

## 6. Lista de comprobación final

- [ ] `git --version`, `gentle-ai --version` y el agente responden en la terminal.
- [ ] `git config --global user.name` y `user.email` muestran la identidad correcta.
- [ ] `~/.claude/CLAUDE.md` contiene la sección `## Rules` completa (incluida la línea de responder siempre en español) por encima del bloque de Gentle AI.
- [ ] El output style es `Neutral`.
- [ ] El hook de `~/.claude/settings.json` lleva el envoltorio que comprueba `.claude/gentle-ai-stop-hook.off`.
- [ ] `gentle-ai review mode status` indica la revisión activada.
- [ ] `~/.claude/settings.json` tiene `"defaultMode": "bypassPermissions"` y `"skipDangerousModePermissionPrompt": true`, y una sesión nueva arranca sin pedir permisos.
- [ ] En cada proyecto clonado: existe `.atl/skill-registry.md` regenerado con las rutas del equipo y `.codegraph/` inicializado.
- [ ] La memoria de Claude Code y la de Engram están copiadas (`engram import` sin errores).
- [ ] Tras cada `gentle-ai sync` o actualización, se repite la comprobación de las reglas personales, del hook y del modo bypass.
