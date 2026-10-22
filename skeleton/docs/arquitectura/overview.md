# Visión General de Arquitectura: {{NOMBRE_PROYECTO}}

> Este documento describe la arquitectura técnica fundamental de **{{NOMBRE_PROYECTO}}**, definiendo la organización modular, los límites de responsabilidad entre capas, las reglas de dependencia e inversión de control y el catálogo de Decisiones de Arquitectura (ADR).

> [!NOTE]
> **Estado en Día 0**: Esta estructura y capas representan la arquitectura fundacional acordada para el proyecto. En el Día 0 no se genera código fuente ni se requiere compilar; los directorios y la implementación concreta del código dentro de `{{CARPETA_CODIGO}}/` se inicializan a partir de la Fase 1 del roadmap.

---

## 1. Estructura de Carpetas del Código

El código fuente del proyecto se organiza dentro de `{{CARPETA_CODIGO}}/` siguiendo una separación clara de responsabilidades:

```text
{{CARPETA_CODIGO}}/
├── presentation/          # Capa de Presentación: UI, vistas, widgets, componentes visuales
│   ├── components/        # Componentes y elementos visuales reutilizables
│   ├── screens/           # Pantallas o vistas principales de la aplicación
│   └── theme/             # Definiciones de estilos, paletas y tokens visuales
│
├── application/           # Capa de Aplicación / Estado
│   ├── controllers/       # Controladores, viewmodels, providers o cubits
│   └── usecases/          # Casos de uso o flujos de orquestación de negocio
│
├── domain/                # Capa de Dominio / Negocio puro
│   ├── models/            # Entidades de dominio y objetos de valor (inmutables)
│   └── repositories/      # Interfaces / contratos de repositorios y servicios
│
├── infrastructure/        # Capa de Infraestructura / Datos y Plataforma
│   ├── datasources/       # Acceso a almacenamiento local, APIs, bases de datos
│   ├── repositories/      # Implementaciones concretas de los contratos de dominio
│   └── platform/          # Adaptadores concretos a APIs nativas o del sistema
│
└── shared/                # Utilidades puras, constantes globales y helpers transversales
    ├── constants/
    └── utils/
```

---

## 2. Capas y Responsabilidades

```
┌────────────────────────────────────────────────────────┐
│            1. Presentación (UI / Vistas)               │
└───────────────────────────┬────────────────────────────┘
                            │ usa
┌───────────────────────────▼────────────────────────────┐
│      2. Aplicación (Gestión de Estado / Casos de Uso)  │
└───────────────────────────┬────────────────────────────┘
                            │ usa contratos
┌───────────────────────────▼────────────────────────────┐
│        3. Dominio (Entidades de Negocio puras)         │
└───────────────────────────▲────────────────────────────┘
                            │ implementa contratos
┌───────────────────────────┴────────────────────────────┐
│   4. Infraestructura / Plataforma (IO, DB, OS APIs)   │
└────────────────────────────────────────────────────────┘
```

1. **Capa de Presentación:**
   - Responsable exclusiva del renderizado visual y de capturar interacciones del usuario.
   - No contiene lógica de negocio ni llamadas directas a APIs del sistema operativo o bases de datos.
   - Reacciona a estados emitidos por la capa de aplicación.

2. **Capa de Aplicación / Estado:**
   - Modela y administra el estado de las pantallas y flujos de usuario.
   - Orquesta la ejecución de casos de uso invocando contratos de la capa de dominio.
   - Es independiente de los detalles de renderizado (fácilmente testeable sin montar UI completa).

3. **Capa de Dominio / Datos:**
   - Corazón del sistema; contiene modelos de datos, reglas de validación y abstracciones de repositorio (*interfaces / abstract classes*).
   - No depende de ninguna librería externa, framework de UI ni de APIs nativas. Código puramente agnóstico.

4. **Capa de Infraestructura y Plataforma:**
   - Proporciona implementaciones reales a los contratos de dominio (lectura de archivos, SQLite/SharedPreferences, sensores, servicios nativos).
   - Aísla los detalles volátiles y dependientes del sistema operativo.

---

## 3. Reglas de Dependencias y Testabilidad

Para garantizar un código mantenible, desacoplado y 100% verificable mediante pruebas automáticas:

- **Regla de Dependencia Unidireccional:** Las capas superiores dependen de las abstracciones de las capas inferiores. El dominio **nunca** depende de infraestructura ni de presentación.
- **Inversión de Dependencias (DIP):** Todo acceso a recursos del sistema operativo, almacenamiento, red o reloj debe realizarse a través de interfaces declaradas en el dominio o la aplicación.
- **Uso estricto de Fakes / Mocks para Plataforma:**
  - En tests unitarios y de integración nunca se debe invocar la plataforma real ni interactuar con archivos reales del usuario.
  - Para cada servicio de plataforma (`IFileSystemService`, `IPermissionService`, etc.) debe existir una implementación de prueba (`FakeFileSystemService`, `FakePermissionService`) en memoria, predecible y rápida.
- **Mantenibilidad:** El código de negocio debe poder compilarse y ejecutarse en entornos de desarrollo sin requerir hardware o dispositivos físicos conectados.

---

## 4. Registro de Decisiones de Arquitectura (ADR)

Las decisiones técnicas de impacto significativo se documentan formalmente como Architecture Decision Records (ADRs) bajo la carpeta `decisiones/`.

> **Regla de Inmutabilidad:**
> Un ADR en estado **Aceptado** jamás se edita ni se sobrescribe para reflejar un cambio técnico posterior.
> Si una decisión previa queda obsoleta o se modifica el rumbo técnico, se redacta un **nuevo ADR** que explícitamente marca el anterior como **Sustituido por ADR 0001** (o el identificador del nuevo ADR que lo sustituya).

### Registro Histórico

| ID | Título | Fecha | Estado | Resumen |
|:---|:---|:---:|:---:|:---|
| [ADR 0001](decisiones/0001-stack-y-arquitectura-inicial.md) | Stack y Arquitectura Inicial | {{FECHA_INICIAL}} | Aceptado | Selección de tecnologías base, plataforma objetivo y estructura modular |
