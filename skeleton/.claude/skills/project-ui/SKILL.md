---
name: project-ui
description: Reglas de oro, directrices de diseño y patrones de interfaz de usuario para {{NOMBRE_PROYECTO}}. Usar siempre al crear o modificar componentes visuales, pantallas o estilos.
---

# Skill: Directrices de UI/UX — {{NOMBRE_PROYECTO}}

Esta skill define las restricciones mandatorias de diseño visual e implementación de interfaz para {{NOMBRE_PROYECTO}}. Cualquier agente o subagente que construya pantallas o widgets debe consultar y cumplir estas directrices antes de emitir código.

---

## 1. Reglas de Oro Inviolables

1. **Cero colores hardcodeados:**  
   Nunca uses literales de color (por ejemplo `Color(0xFF...)`, `#FFFFFF`, `rgba(...)`). Todos los colores deben obtenerse exclusivamente de los tokens semánticos del tema centralizado en `design/DESIGN.md` y la definición de tema del proyecto.

2. **Cero textos literales (Strings quemados):**  
   Ninguna vista, diálogo o botón puede contener texto plano quemado en el código fuente. Todos los textos visibles deben registrarse en el archivo de localización y consumirse mediante el helper o servicio de l10n correspondiente.

3. **No inventar pantallas ni botones:**  
   La interfaz se limita estrictamente a lo especificado en `docs/producto/requisitos.md` y a la fase actualmente abierta en `docs/plan/roadmap.md`. Aunque una maqueta o captura contenga botones adicionales, si no figuran en los requisitos aprobados, **no se implementan**.

4. **Zonas táctiles accesibles (Ergonomía mínima):**  
   Todo control interactivo (botones, iconos táctiles, checkboxes, conmutadores) debe contar con una superficie de toque mínima de **48x48dp** (o puntos lógicos equivalentes), independientemente del tamaño visual del icono interno.

5. **Manejo obligatorio de los 3 estados de pantalla:**  
   Cualquier vista que presente información dinámica o asíncrona debe implementar de forma explícita:
   - **Cargando:** Spinner o skeleton loader centrado y no intrusivo.
   - **Vacío:** Estado vacío informativo con llamada a la acción clara cuando no hay registros.
   - **Error:** Retroalimentación comprensible sin tecnicismos y botón de reintento.

---

## 2. Tipografía y Espaciado

- **Jerarquía:** No mezcles estilos arbitrarios (`fontSize: 17.3`). Respeta la escala tipográfica documentada en `design/DESIGN.md` (Display, H1, H2, Body, Caption).
- **Márgenes y Padding:** Emplea siempre la cuadrícula basada en 4px/8px (8px, 16px, 24px, 32px). Mantén un padding lateral constante de 16px en las vistas estándar.

---

## 3. Checklist de Verificación de UI antes de Entregar

Antes de dar por completado un componente o vista, verifica:
- [ ] ¿Todos los colores proceden de tokens semánticos del tema?
- [ ] ¿Se ven legibles tanto en modo claro como en modo oscuro?
- [ ] ¿Todos los textos provienen de internacionalización (l10n)?
- [ ] ¿El área de pulsación de botones e iconos es de al menos 48x48dp?
- [ ] ¿La pantalla gestiona adecuadamente estados de carga, error y vacío?
- [ ] ¿Cumple estrictamente los requisitos funcionales de la fase activa sin añadir elementos extras?

---

## Related skills (installed in `.claude/skills/`)

- `material-design`: generic Material 3 decisions (card vs text, hierarchy, component choice); this skill and DESIGN.md win on conflict.
- `flutter-build-responsive-layout`: adaptive sizing and constraints.
- `flutter-fix-layout-issues`: overflow and unbounded-constraint errors.
- `flutter-add-widget-test`: `WidgetTester` patterns.

