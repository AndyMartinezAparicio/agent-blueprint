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

## 4. Incidencias y Pendientes Conocidos (Deuda Técnica)

> **Espacio único y canónico:** Anote aquí cualquier problema de entorno, incompatibilidad temporal de librerías, advertencia no resuelta o deuda técnica identificada para no dispersar notas sueltas en el código.

| Fecha | Identificador / Área | Descripción | Impacto / Mitigación temporal | Estado |
|:---:|:---|:---|:---|:---:|
| {{FECHA}} | Entorno / Build | {{DESCRIPCION_INCIDENCIA}} | {{MITIGACION}} | Abierto |
| {{FECHA}} | Rendimiento | {{DESCRIPCION_DEUDA}} | {{MITIGACION}} | En seguimiento |
