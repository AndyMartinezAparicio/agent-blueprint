# Perfil: [Nombre de la Plataforma o Stack]

> [!NOTE]
> Esta es una plantilla base para definir nuevos perfiles de plataforma en `agent-blueprint` (por ejemplo: `web-app.md`, `desktop-app.md`, `backend-api.md`).
> Las secciones a continuación son las esperadas de forma canónica por el protocolo `skeleton/BOOTSTRAP.md` para inyectar reglas técnicas y de calidad en el nuevo proyecto.
> Sustituye los textos entre corchetes con las especificaciones concretas de tu stack.

---

## 1. Reglas Transversales de Plataforma

<!--
Define aquí las políticas regulatorias, normativas de tiendas o navegadores, directrices de compatibilidad o estándares mandatorios de la plataforma.
Ejemplo: Políticas de Google Play / App Store, políticas de cookies y RGPD para Web, firmas de código y certificados para Desktop.
-->

1. **[Regla normativa o de política 1]**: [Descripción detallada de la política o restricción que debe contrastarse antes de codificar].
2. **[Regla normativa o de política 2]**: [Criterios para detectar riesgo de rechazo, penalización de SEO o fallas de distribución].
3. **[Principio de compatibilidad o estándares]**: [Estándares mandatorios, compatibilidad mínima con versiones de SO o navegadores soportados].

---

## 2. Privacidad y Seguridad por Defecto

<!--
Especifica cómo se manejan los datos del usuario, el cifrado, los permisos del sistema operativo y los vectores de ataque comunes en este ecosistema.
-->

1. **Gestión de datos y privacidad**: [Políticas sobre dónde se procesan los datos: en local, nube, recolección de telemetría, etc.].
2. **Permisos y capacidades mínimas**: [Reglas sobre qué permisos se solicitan y cómo se manejan situaciones de rechazo o revocación].
3. **Almacenamiento y transporte seguro**: [Mecanismos obligatorios para almacenar credenciales locales o comunicarse por red de forma segura].

---

## 3. Atributos de Calidad Específicos

<!--
Detalla los requisitos no funcionales adaptados a esta tecnología: UX, rendimiento, fiabilidad y accesibilidad.
-->

### Usabilidad y Experiencia de Usuario (UX)
- **[Directriz de interacción 1]**: [Manejo de navegación, estados vacíos, feedback de carga o confirmación de acciones destructivas].
- **[Directriz de interacción 2]**: [Adaptabilidad al tamaño de pantalla, ventanas flotantes, atajos de teclado o gestos].

### Rendimiento y Recursos
- **[Métricas de rendimiento]**: [Objetivos concretos: tiempos de carga inicial (FCP, LCP), consumo de memoria RAM, cuotas de red o fps esperados].
- **[Gestión de colecciones y datos]**: [Estrategia de paginación, virtualización de listas o carga diferida].

### Fiabilidad y Manejo de Errores
- **[Resiliencia ante fallos]**: [Comportamiento offline, reconexión ante caídas de red, gestión de sesiones expiradas].
- **[Manejo del ciclo de vida]**: [Comportamiento al suspender la ventana, cambiar de pestaña o perder foco del sistema].

### Accesibilidad (a11y)
- **[Estándar de accesibilidad]**: [Nivel WCAG requerido (ej. WCAG 2.1 AA), soporte para lectores de pantalla (ARIA, Semantics)].
- **[Contraste y navegación por teclado]**: [Foco visible, navegación completa por teclado y áreas interactivas mínimas].

---

## 4. Entorno de Desarrollo y Restricciones

<!--
Indica las restricciones de herramientas locales, uso de emuladores, hardware de pruebas requerido o limitaciones de disco/memoria en la máquina de desarrollo.
-->

1. **Hardware y dispositivos de prueba**: [Especifica si se prueban en navegadores reales, dispositivos físicos por USB o emuladores autorizados].
2. **Restricciones de espacio y dependencias**: [Directrices sobre qué SDKs, paquetes globales o imágenes se pueden o no instalar en la máquina local].

---

## 5. Comandos de Validación Pre-Commit

<!--
Lista los comandos deterministas que el desarrollador o el agente deben ejecutar antes de cada commit para asegurar que el proyecto está 100% libre de advertencias y regresiones.
-->

```bash
# 1. Linter y análisis estático (0 advertencias y 0 errores)
[comando de lint / análisis]

# 2. Comprobación de tipos / compilación
[comando de build o typecheck]

# 3. Batería de pruebas automatizadas (100% en verde)
[comando de tests unitarios e integración]
```

---

## 6. Skills Recomendadas para el Agente

<!--
Menciona las skills especializadas, extensiones o herramientas automáticas que el agente de IA debe utilizar al trabajar en este perfil.
-->

| Skill | Finalidad |
| :--- | :--- |
| `[nombre-skill-1]` | [Propósito y caso de uso dentro de la plataforma]. |
| `[nombre-skill-2]` | [Propósito y caso de uso dentro de la plataforma]. |
| `[nombre-skill-3]` | [Propósito y caso de uso dentro de la plataforma]. |
