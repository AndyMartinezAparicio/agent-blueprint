# Documentación de {{NOMBRE_PROYECTO}}

Bienvenido al repositorio documental central de **{{NOMBRE_PROYECTO}}**. Toda la documentación de este proyecto sigue estrictamente el principio rector:

> **"Un dato vive en un solo sitio" (Single Source of Truth - SSOT)**
>
> Para evitar inconsistencias, desactualizaciones y confusión:
> - Si un dato (visión, requisito, decisión, estado de fase, regla de arquitectura) cambia, se actualiza **únicamente en su documento canónico**.
> - Ningún otro documento debe duplicar información detallada; debe enlazar directamente a la fuente original.

---

## Estructura y Navegación

A continuación se detalla el mapa de documentos y la responsabilidad exclusiva de cada uno:

### 1. Producto y Requisitos
* [Visión del Producto](producto/vision.md): Define el problema real, la propuesta de valor única, los principios de privacidad/seguridad, el modelo de producto v1.0 y los requisitos transversales de plataforma.
* [Requisitos Funcionales](producto/requisitos.md): Catálogo exhaustivo y numerado (`RF-01`, `RF-02`...) de los requisitos del sistema, organizado por módulos, junto con la sección explícita de elementos fuera de alcance (*out of scope*).

### 2. Arquitectura y Decisiones Técnicas
* [Visión General de Arquitectura](arquitectura/overview.md): Estructura de directorios del código, modelo de capas, reglas de dependencias, desacoplamiento de plataforma y registro global de decisiones arquitectónicas.
* [Registro de Decisiones Arquitectónicas (ADRs)](arquitectura/decisiones/): Historial inmutable de decisiones técnicas clave tomadas a lo largo de la vida del proyecto.
  * [Plantilla de ADR](arquitectura/decisiones/_TEMPLATE-adr.md): Formato estándar para proponer y documentar nuevas decisiones.
  * [ADR 0001: Stack y Arquitectura Inicial](arquitectura/decisiones/0001-stack-y-arquitectura-inicial.md): Selección inicial de tecnologías, plataforma objetivo y fundamentos arquitectónicos.

### 3. Planificación, Roadmap y Fases
* [Roadmap del Proyecto](plan/roadmap.md): **Único lugar** donde reside el estado oficial de avance de cada fase (*Pendiente*, *En curso*, *Aprobada*), versiones asociadas y reglas de release/fusión.
* [Fases de Desarrollo](plan/fases/): Especificaciones detalladas de alcance y criterios de aceptación por fase.
  * [Plantilla de Fase](plan/fases/_TEMPLATE-fase.md): Estructura canónica para desglosar cada fase (alcance, requisitos cubiertos, criterios de aceptación verificables y riesgos).

### 4. Guías Operativas y Flujo de Trabajo
* [Guía de Desarrollo](guias/desarrollo.md): Configuración del entorno local, comandos habituales del día a día, convenciones de tests/código e inventario de incidencias o deuda técnica conocida.
* [Changelog / Registro de Cambios](CHANGELOG.md): Historial de versiones y cambios del proyecto basado en *Keep a Changelog* y *Semantic Versioning*.

### 5. Diseño y Sistema Visual
* [Sistema de Diseño](../design/DESIGN.md): Directrices visuales, tokens de diseño, paleta cromática, tipografías, componentes y reglas de experiencia de usuario.

---

## Reglas de Mantenimiento Documental

1. **Mantener viva la documentación**: Toda nueva funcionalidad o cambio de alcance debe reflejarse en los documentos antes o durante el ciclo de desarrollo correspondiente.
2. **Inmutabilidad de los ADRs**: Un ADR aceptado jamás se edita para alterar su contenido histórico. Si la decisión cambia, se crea un nuevo ADR que sustituye formalmente al anterior.
3. **Control de versiones**: Las versiones definitivas de la documentación deben avanzar en sincronía con los tags y releases en la rama principal (`main`).
