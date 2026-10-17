# Sistema de Diseño Visual — {{NOMBRE_PROYECTO}}

---

## Notas del proyecto (PREVALECE SOBRE EL RESTO DEL DOCUMENTO)

> **REGLAS DE PREVALENCIA Y DIRECTRICES INVIOLABLES:**
>
> 1. **Separación estricta entre diseño y función:**  
>    Este documento (`DESIGN.md`) y cualquier mockup, captura o wireframe ubicado en `design/screens/` definen **exclusivamente el aspecto visual, disposición de elementos, tokens y ergonomía de interfaz**.  
>    Las funcionalidades, flujos de navegación, pantallas activas, reglas de negocio y textos provienen **única y exclusivamente de `docs/producto/requisitos.md`** y la fase abierta en `docs/plan/roadmap.md`. Jamás implementes un botón, acción o pantalla simplemente porque aparezca en una captura si no está respaldado en la documentación funcional.
>
> 2. **Paleta centralizada en archivo único de tokens:**  
>    Queda terminantemente prohibido utilizar valores de color hardcodeados (como `Color(0xFF...)`, `#hex` o `rgb(...)`) de forma dispersa en los componentes o vistas. Todos los colores deben consumirse a través del archivo centralizado de tokens del tema:  
>    `{{ARCHIVO_PALETA}}`
>
> 3. **Internacionalización y textos centralizados:**  
>    Ningún widget o vista debe contener cadenas de texto literales (strings quemados en código). Todos los textos deben definirse y consumirse a través del sistema oficial de internacionalización:  
>    `{{SISTEMA_L10N}}`
>
> 4. **Notas visuales específicas de pantallas:**  
>    {{NOTAS_VISUALES_PROYECTO}}

---

## 1. Paleta de Colores y Tokens Semánticos

El sistema de diseño define roles semánticos universales compatibles con modo claro y modo oscuro.

### Modo Claro (*Light Theme*)

| Token Semántico | Valor Hex / Referencia | Rol de Uso |
| :--- | :--- | :--- |
| `background` | `#F8F9FA` | Fondo principal de pantallas |
| `surface` | `#FFFFFF` | Fondo de tarjetas, hojas inferiores y contenedores elevados |
| `surfaceVariant` | `#F1F3F5` | Fondo de elementos secundarios o campos inactivos |
| `primary` | `#1A73E8` | Color de acento de marca, botones principales y estados activos |
| `onPrimary` | `#FFFFFF` | Texto o iconos sobre fondo `primary` |
| `textPrimary` | `#202124` | Texto principal, encabezados y títulos |
| `textSecondary` | `#5F6368` | Subtítulos, etiquetas secundarias y textos de apoyo |
| `border` | `#DADCE0` | Bordes sutiles y divisores estructurales |
| `error` | `#D93025` | Mensajes y estados de error |
| `success` | `#1E8E3E` | Confirmaciones de éxito y estados positivos |

### Modo Oscuro (*Dark Theme*)

| Token Semántico | Valor Hex / Referencia | Rol de Uso |
| :--- | :--- | :--- |
| `background` | `#121212` | Fondo principal de pantallas en modo oscuro |
| `surface` | `#1E1E1E` | Contenedores elevados y tarjetas |
| `surfaceVariant` | `#2C2C2C` | Elementos de apoyo y divisores destacados |
| `primary` | `#8AB4F8` | Acento optimizado para contraste en fondos oscuros |
| `onPrimary` | `#121212` | Texto o iconos sobre color `primary` |
| `textPrimary` | `#E8EAED` | Texto principal legible |
| `textSecondary` | `#9AA0A6` | Textos secundarios y metadatos |
| `border` | `#3C4043` | Líneas divisorias en modo oscuro |
| `error` | `#F28B82` | Alertas de error con alto contraste |
| `success` | `#81C995` | Estados de éxito |

---

## 2. Tipografía y Jerarquía Textual

La tipografía debe mantener legibilidad óptima y jerarquía uniforme en toda la aplicación.

- **Familia principal:** Fuente del sistema (o tipografía definida en el perfil).
- **Escala tipográfica:**
  - **Título 1 (H1 / Display):** `28px` — Peso: Semibold / Bold (700) — Altura de línea: `34px`.
  - **Título 2 (H2 / Pantalla):** `22px` — Peso: Semibold (600) — Altura de línea: `28px`.
  - **Título 3 (H3 / Sección):** `18px` — Peso: Medium (500) — Altura de línea: `24px`.
  - **Cuerpo Principal (Body Regular):** `15px` — Peso: Regular (400) — Altura de línea: `22px`.
  - **Cuerpo Secundario (Body Small):** `13px` — Peso: Regular (400) — Altura de línea: `18px`.
  - **Subtítulo / Metadatos (Caption):** `11px` — Peso: Regular / Medium (400-500) — Altura de línea: `16px`.

---

## 3. Espaciado y Cuadrícula

Se adopta una cuadrícula base con escala de múltiplos de **4px / 8px**:

- `spacing-xs`: `4px` (espaciados internos mínimos entre icono y etiqueta)
- `spacing-sm`: `8px` (separación compacta entre elementos afines)
- `spacing-md`: `16px` (margen estándar horizontal de pantallas y padding de tarjetas)
- `spacing-lg`: `24px` (separación vertical entre secciones)
- `spacing-xl`: `32px` (márgenes amplios de cabeceras o llamadas a la acción)

### Radios de Borde (Corner Radii)
- **Elementos pequeños (badges, tags, chips):** `6px` a `8px`.
- **Botones y campos de texto:** `10px` a `12px`.
- **Tarjetas y contenedores (Cards):** `16px`.
- **Hojas modales inferiores (Bottom Sheets):** `24px` en las esquinas superiores.

---

## 4. Componentes del Sistema

### Botones
- **Botón Primario:** Fondo `primary`, texto `onPrimary`, altura mínima de `48px`, borde redondeado (`10px`).
- **Botón Secundario / Outlined:** Fondo transparente, borde de `1px` en `primary` o `border`, texto `textPrimary`.
- **Zonas Táctiles:** Cada elemento interactivo debe poseer un área de pulsación mínima de **48x48dp**, garantizando accesibilidad ergonómica.

### Tarjetas (Cards)
- Fondo `surface`, bordes de `1px` con token `border` o elevación sutil sin sombras duras.
- Padding interno estándar de `16px`.

### Diálogos y Modales
- Presentación limpia, con fondo atenuado (overlay), títulos concisos, acciones destructivas destacadas en `error` y botón de descarte/cancelación accesible.

### Estados de Vista Obligatorios
Toda pantalla que cargue o visualice colecciones de datos debe contemplar explícitamente:
1. **Estado de Carga:** Indicador visual de progreso centrado o efecto skeleton.
2. **Estado Vacío:** Ilustración o icono sutil, texto explicativo claro y botón de acción sugerida.
3. **Estado de Error:** Mensaje amistoso con causa legible y botón de reintento.
