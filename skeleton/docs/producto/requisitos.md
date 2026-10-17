# Requisitos del Producto: {{NOMBRE_PROYECTO}}

> Este documento es la fuente canónica para los requisitos funcionales de **{{NOMBRE_PROYECTO}}**. 
> Cada requisito cuenta con un identificador unívoco (`RF-XX`) que se referencia en las fases del roadmap, tareas y pruebas unitarias/de integración.

---

## 1. Convenciones y Estados

- **Identificador:** `RF-XX` (secuencial de dos o más dígitos).
- **Prioridad:**
  - `Alta (Must Have)`: Imprescindible para el funcionamiento nuclear de la v1.0.
  - `Media (Should Have)`: Muy recomendable, aporta alto valor, postergable solo si bloquea entrega.
  - `Baja (Nice to Have)`: Deseable si el tiempo y recursos lo permiten sin comprometer la fecha.

---

## 2. Requisitos Funcionales por Bloque Temático

### Bloque A: Inicialización y Configuración

#### RF-01: {{TITULO_RF_01}}
- **Prioridad:** Alta (Must Have)
- **Descripción:** {{DESCRIPCION_DETALLADA_RF_01}}
- **Criterio de Aceptación:**
  - [ ] {{CRITERIO_VERIFICABLE_1}}
  - [ ] {{CRITERIO_VERIFICABLE_2}}

#### RF-02: {{TITULO_RF_02}}
- **Prioridad:** Alta (Must Have)
- **Descripción:** {{DESCRIPCION_DETALLADA_RF_02}}
- **Criterio de Aceptación:**
  - [ ] {{CRITERIO_VERIFICABLE_1}}
  - [ ] {{CRITERIO_VERIFICABLE_2}}

---

### Bloque B: Funcionalidad Nuclear (Core)

#### RF-03: {{TITULO_RF_03}}
- **Prioridad:** Alta (Must Have)
- **Descripción:** {{DESCRIPCION_DETALLADA_RF_03}}
- **Criterio de Aceptación:**
  - [ ] {{CRITERIO_VERIFICABLE_1}}
  - [ ] {{CRITERIO_VERIFICABLE_2}}

#### RF-04: {{TITULO_RF_04}}
- **Prioridad:** Media (Should Have)
- **Descripción:** {{DESCRIPCION_DETALLADA_RF_04}}
- **Criterio de Aceptación:**
  - [ ] {{CRITERIO_VERIFICABLE_1}}
  - [ ] {{CRITERIO_VERIFICABLE_2}}

---

### Bloque C: Gestión de Datos y Persistencia

#### RF-05: {{TITULO_RF_05}}
- **Prioridad:** Alta (Must Have)
- **Descripción:** {{DESCRIPCION_DETALLADA_RF_05}}
- **Criterio de Aceptación:**
  - [ ] {{CRITERIO_VERIFICABLE_1}}
  - [ ] {{CRITERIO_VERIFICABLE_2}}

---

### Bloque D: Interfaz y Experiencia de Usuario (UI/UX)

#### RF-06: {{TITULO_RF_06}}
- **Prioridad:** Media (Should Have)
- **Descripción:** {{DESCRIPCION_DETALLADA_RF_06}}
- **Criterio de Aceptación:**
  - [ ] {{CRITERIO_VERIFICABLE_1}}
  - [ ] {{CRITERIO_VERIFICABLE_2}}

---

## 3. Fuera del Alcance de la v1.0 (Out of Scope)

> **Importante para mitigar la desviación de alcance (*Scope Creep*):**
> Las siguientes características están explícitamente excluidas de la versión 1.0. No deben implementarse ni generar dependencias durante las fases iniciales, salvo que se apruebe una revisión formal del roadmap.

- **{{FUNCIONALIDAD_EXCLUIDA_1}}**: {{MOTIVO_EXCLUSION_1}} (p. ej. sincronización automática multi-dispositivo en la nube; se evaluará para v2.0).
- **{{FUNCIONALIDAD_EXCLUIDA_2}}**: {{MOTIVO_EXCLUSION_2}} (p. ej. sistema de cuentas de usuario y login federado; la v1.0 opera en modo local).
- **{{FUNCIONALIDAD_EXCLUIDA_3}}**: {{MOTIVO_EXCLUSION_3}} (p. ej. integración con pasarelas de pago externas o suscripciones complejas).
- **{{FUNCIONALIDAD_EXCLUIDA_4}}**: {{MOTIVO_EXCLUSION_4}} (p. ej. internacionalización en más de 2 idiomas iniciales).
