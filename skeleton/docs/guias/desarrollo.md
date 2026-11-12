# Guía de Desarrollo: {{NOMBRE_PROYECTO}}

> Este documento contiene las instrucciones prácticas para configurar el entorno local, ejecutar los comandos habituales de desarrollo, seguir las convenciones de código y registrar incidencias o deuda técnica conocida.

---

## 1. Entorno del Desarrollador

- **Sistema Operativo:** {{SISTEMA_OPERATIVO}} (p. ej. Windows 11 / macOS / Linux)
- **Runtime / SDK:** {{RUNTIME_VERSION}} (p. ej. Flutter SDK X.Y.Z / Node.js XX / Python 3.XX)
- **Herramientas y CLI requeridas:**
  - Git
  - {{HERRAMIENTA_CLI_1}}
  - {{HERRAMIENTA_CLI_2}}
- **Restricciones de disco y herramientas:**
  - Evitar escrituras masivas o caches temporales descontroladas fuera del directorio de build/caché estándar.
  - Asegurar que `.gitignore` excluya dependencias, carpetas temporales de compilación y artefactos generados.
- **Modo de ejecución y pruebas locales:**
  - La lógica de negocio y aplicación debe poder ejecutarse y probarse 100% en local sin emuladores pesados ni hardware conectado.
  - Para pruebas visuales completas o integración nativa, utilizar: {{METODO_EJECUCION_DEV}} (p. ej. emulador Android, simulador iOS o build de escritorio).

---

## 2. Comandos Habituales

A continuación se detallan los comandos estándar para el ciclo de vida de desarrollo:

### 2.1. Instalación de dependencias
```bash
{{COMANDO_INSTALAR_DEPENDENCIAS}}
# Ejemplo: flutter pub get / npm install / poetry install
```

### 2.2. Ejecución de la aplicación en desarrollo
```bash
{{COMANDO_EJECUTAR_APP}}
# Ejemplo: flutter run -d chrome / npm run dev / python main.py
```

### 2.3. Linter y análisis estático
```bash
{{COMANDO_LINTER}}
# Ejemplo: flutter analyze / npm run lint / ruff check .
```
> **Criterio estricto:** El código no debe tener ningún error ni advertencia del linter antes de hacer commit.

### 2.4. Ejecución de pruebas automáticas
```bash
# Ejecutar toda la suite de tests
{{COMANDO_TESTS}}
# Ejemplo: flutter test / npm test / pytest

# Ejecutar tests con reporte de cobertura
{{COMANDO_TESTS_COBERTURA}}
# Ejemplo: flutter test --coverage / npm test -- --coverage
```

---

## 3. Convenciones de Código y Tests

- **Test-First (TDD) en lógica de negocio:**
  - Cuando se implemente un cálculo, validador, transformación de datos o caso de uso, se escriben primero los tests unitarios con los casos borde y luego la implementación mínima necesaria.
- **Desacoplamiento estricto de plataforma:**
  - **Prohibido** interactuar directamente con el sistema de archivos real, sensores, GPS, red o almacenamiento nativo en tests automáticos.
  - Utilizar siempre implementaciones falsas en memoria (*Fakes*) que implementen la misma interfaz que el servicio real.
- **Nomenclatura limpia y consistente:**
  - Clases en `PascalCase`.
  - Funciones, métodos y variables en `camelCase` (o `snake_case` según el lenguaje del stack).
  - Archivos de test nombrados con sufijo `_test` o `.test` reflejando el path del archivo probado.
- **Manejo de errores explícito:**
  - No silenciar excepciones. Modelar resultados de error de forma tipada (`Result<T, E>`, `Either` o excepciones de dominio bien definidas).

---

## 4. Antes de Cada Commit

- Mientras se trabaja, ejecuta solo el linter y los tests del módulo que se toca.
- La suite completa ({{COMANDO_TESTS}}) se ejecuta **una vez antes de cada commit**, no tras cada cambio.
- El agente no compila, ejecuta ni instala la aplicación sin permiso del usuario: compila el usuario.
- Las pruebas que requieren dispositivo real se apuntan en [`docs/plan/pruebas-pendientes.md`](../plan/pruebas-pendientes.md).

---

## 5. Equipo Nuevo con Gentle AI

Lo que viaja con el repositorio (`AGENTS.md`, `.claude/skills/`, `.gitattributes`, `.claude/gentle-ai-stop-hook.off`) no hay que configurarlo. Tras instalar Claude Code y Gentle AI en un equipo nuevo, se pide al agente:

1. **Estilo de respuesta:** poner el output style en `Neutral`.
2. **Reglas personales** en la sección `## Rules` de `~/.claude/CLAUDE.md`, por encima del bloque de Gentle AI: sin `Co-Authored-By` ni atribución de IA y con Conventional Commits; respuestas cortas; una sola pregunta cada vez; sin menús de opciones salvo elección real; verificar antes de dar la razón; responder siempre en español.
3. **Aviso de revisión al final de cada respuesta:** en `~/.claude/settings.json`, envolver el hook `gentle-ai review stop-hook` para que salga sin hacer nada si existe `.claude/gentle-ai-stop-hook.off` en el proyecto:
   `if [ -f "${CLAUDE_PROJECT_DIR:-.}/.claude/gentle-ai-stop-hook.off" ]; then cat >/dev/null; exit 0; fi; exec gentle-ai review stop-hook --agent claude-code`.
   Repetirlo tras cada `gentle-ai sync` o actualización.
4. **Por cada proyecto clonado:** `gentle-ai skill-registry refresh` (sus rutas son de cada equipo) y `gentle-ai codegraph init --cwd <proyecto>`.
5. **Revisión nativa:** comprobar `gentle-ai review mode status` (activada por defecto).
6. **Git global:** `user.name` y `user.email` iguales que en el otro equipo.
7. **Modo bypass de permisos:** en `~/.claude/settings.json`, `"permissions": { "defaultMode": "bypassPermissions" }` y `"skipDangerousModePermissionPrompt": true`. El agente no pide permiso para cada comando; los límites (git, borrados, compilar) los ponen las reglas de `AGENTS.md`. Usarlo solo en el equipo personal.

Y se copia del equipo anterior:

8. **Memoria de Claude Code:** `~/.claude/projects/<proyecto>/memory/` de cada proyecto (el nombre de la carpeta depende de la ruta del proyecto).
9. **Memoria de Engram:** `engram export engram-export.json --all` en el equipo viejo y `engram import engram-export.json` en el nuevo.

---

## 6. Incidencias y Pendientes Conocidos (Deuda Técnica)

> **Espacio único y canónico:** Anote aquí cualquier problema de entorno, incompatibilidad temporal de librerías, advertencia no resuelta o deuda técnica identificada para no dispersar notas sueltas en el código.

| Fecha | Identificador / Área | Descripción | Impacto / Mitigación temporal | Estado |
|:---:|:---|:---|:---|:---:|
<!-- Formato de ejemplo: | AAAA-MM-DD | Entorno / Build | Incompatibilidad temporal de librerías | Fijar versión específica en configuración | Abierto | -->
| - | - | *Sin incidencias ni deuda técnica registrada en la inicialización (Día 0).* | Ninguno | N/A |
