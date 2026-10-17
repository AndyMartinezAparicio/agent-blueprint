# Perfil: Móvil con Flutter y Publicación en Tiendas (Google Play / App Store)

Este perfil define las directrices técnicas, normativas y de calidad para aplicaciones móviles desarrolladas con **Flutter** cuyo destino final sea la distribución oficial a través de tiendas como **Google Play Store** o **Apple App Store**.

> [!IMPORTANT]
> Este perfil condensa las lecciones aprendidas y mejores prácticas del proyecto *Purge*. Al inicializar un proyecto con este perfil mediante `skeleton/BOOTSTRAP.md`, estas reglas deben integrarse en el `AGENTS.md`, `docs/desarrollo.md` y `docs/requerimientos/sistema.md` del nuevo repositorio.

---

## 1. Reglas Transversales de Google Play y Políticas de Tienda

1. **Verificación previa a la codificación**: Toda decisión técnica que involucre capacidades sensibles del sistema operativo debe contrastarse con la documentación oficial vigente de Google Play Console antes de escribir una sola línea de código. Esto incluye de forma no limitativa:
   - Permisos de almacenamiento y medios (`READ_MEDIA_IMAGES`, `READ_MEDIA_VIDEO`, `MANAGE_EXTERNAL_STORAGE`).
   - Gestión de archivos y Scoped Storage / Photo Picker del sistema.
   - Acceso a ubicación en segundo plano o servicios en primer plano (`Foreground Service`).
   - Redes de anuncios, SDKs de analítica y mecanismos de compras in-app (Google Play Billing).
   - Notificaciones push y permisos en tiempo de ejecución de Android 13+.
2. **Alerta de riesgo de rechazo**: Si una funcionalidad solicitada o un diseño preliminar entra en conflicto con las directrices de la tienda o acarrea riesgo de rechazo durante la revisión de Google Play, **el agente debe detener la implementación, alertar al desarrollador explícitamente y proponer alternativas conformes a las políticas**.
3. **Mínimo privilegio de permisos**: Nunca se solicitarán permisos generales si existe una API de sistema que resuelva el caso de uso sin permisos (por ejemplo, usar el selector de fotos del sistema `ActivityResultContracts.PickVisualMedia` en vez de solicitar acceso a toda la galería).

---

## 2. Privacidad y Seguridad por Defecto

1. **Procesamiento en el dispositivo (On-Device First)**: Todo análisis, indexación, procesamiento de imágenes o metadata debe ejecutarse localmente en el dispositivo del usuario siempre que sea técnicamente viable. Ningún dato privado se transmitirá a servidores externos sin consentimiento explícito y justificación de producto.
2. **Acciones destructivas protegidas**:
   - Cualquier eliminación o alteración de archivos del usuario (fotos, vídeos, documentos) debe canalizarse preferentemente a través de la papelera del sistema (`createTrashRequest` en Android MediaStore) o de un diálogo de confirmación explícito del sistema operativo.
   - Las operaciones destructivas nunca deben implementarse antes de la fase del roadmap dedicada específicamente a ellas.
3. **Persistencia local segura**: Las credenciales, tokens o preferencias confidenciales deben almacenarse utilizando almacenamiento cifrado seguro de la plataforma (`flutter_secure_storage` o Keystore/Keychain).

---

## 3. Atributos de Calidad Específicos para Móvil

### Usabilidad y UX Móvil
- **Gestos complementados con controles visibles**: Los gestos de deslizamiento (swipe, pinch, arrastre) son atajos de conveniencia; jamás deben ser la única forma de ejecutar una acción crítica. Toda acción debe contar con un botón o control visual accesible.
- **Estados vacíos comprensibles**: Si una pantalla o lista carece de contenido, debe mostrar un estado vacío informativo que oriente al usuario sobre el siguiente paso a seguir.
- **Feedback inmediato y confirmación**: Las acciones que toman tiempo deben reflejar indicadores de carga o esqueletos (*skeleton loaders*). Toda acción destructiva o irreversible exige confirmación explícita con botón destructivo diferenciado.

### Rendimiento y Recursos
- **Paginación y carga por lotes**: Queda estrictamente prohibido cargar colecciones completas (álbumes enteros, listas de cientos de archivos, registros de base de datos no paginados) en memoria. Se deben implementar consultas paginadas o cursores en lotes de tamaño razonable (por ejemplo, 50 a 100 elementos).
- **Fluidez visual constante**: Mantener una tasa de refresco fluida a 60 fps (o 120 fps en dispositivos de alta tasa) sin *jank*. Los cálculos pesados deben despacharse a *isolates* de Dart o tareas en background.
- **Eficiencia energética**: Cuidar el consumo de batería; cancelar suscripciones de streams, temporizadores y escuchas de sensores cuando los widgets se desmonten (`dispose()`).

### Fiabilidad y Manejo del Ciclo de Vida
- **Permisos dinámicos y revocados**: La aplicación debe responder con elegancia si el usuario revoca permisos desde los Ajustes del sistema operativo en cualquier momento, o si otorga acceso parcial ("Seleccionar fotos" en Android 14+ / iOS 14+).
- **Consistencia ante cambios externos**: Los archivos o datos modificados o eliminados fuera de la aplicación (por ejemplo, desde el explorador de archivos o la app de cámara) deben manejarse sin bloqueos (*crashes*), refrescando el estado reactivamente.
- **Interrupciones del ciclo de vida**: La aplicación debe pausar y reanudar correctamente sus estados cuando el usuario recibe una llamada, cambia de aplicación o el sistema destruye la actividad por falta de memoria RAM.

### Accesibilidad (a11y)
- **Áreas táctiles mínimas**: Todas las áreas interactivas (botones, iconos tocables, elementos de lista) deben tener un tamaño objetivo mínimo de **48x48 dp** según las directrices de Material Design y Android Accessibility Scanner.
- **Semántica para lectores de pantalla**: Todos los elementos interactivos o informativos deben disponer de etiquetas legibles mediante widgets `Semantics` o atributos `tooltip` para TalkBack / VoiceOver.
- **Escalado y contraste**: La interfaz debe respetar la configuración de escalado de fuente del sistema y cumplir con un ratio de contraste mínimo de 4.5:1 para texto normal según WCAG AA.

---

## 4. Entorno de Desarrollo y Restricciones (Windows sin Emulador)

1. **Pruebas exclusivas en dispositivo físico por USB**:
   - Por restricciones de espacio en disco y consumo de hardware en estaciones Windows, **está prohibido instalar SDKs adicionales no acordados, imágenes pesadas del sistema o emuladores de Android Studio sin autorización explícita**.
   - Toda validación interactiva y depuración en vivo se ejecuta sobre un dispositivo móvil físico conectado mediante depuración USB (`adb devices`).
2. **Validación de tests sin emulador**:
   - Las pruebas automatizadas deben diseñarse como **tests unitarios puros** y **widget tests de Flutter**, los cuales corren en milisegundos en la máquina local de desarrollo mediante el motor headless de pruebas de Flutter, sin necesidad de arrancar dispositivos ni emuladores.

---

## 5. Comandos de Validación Pre-Commit

Antes de considerar concluida cualquier tarea o realizar un commit en Git, deben ejecutarse y aprobarse sin excepción los siguientes comandos:

```bash
# 1. Análisis estático del código Dart/Flutter (debe reportar 0 errores y 0 warnings)
flutter analyze

# 2. Batería completa de pruebas unitarias y de widgets en el entorno local (100% en verde)
flutter test

# 3. Pruebas unitarias de código nativo Android / Kotlin (obligatorio si se modifica android/)
./gradlew.bat :app:testDebugUnitTest
```

---

## 6. Skills Recomendadas para el Agente

Para acelerar el desarrollo y mantener la calidad del código, el agente debe apoyarse en las siguientes skills o capacidades especializadas:

| Skill | Finalidad |
| :--- | :--- |
| `flutter-add-widget-test` | Generación de pruebas automatizadas de widgets con verificación de bombeo de frames (`pumpAndSettle`), interacción táctil y aserciones de estado. |
| `flutter-build-responsive-layout` | Construcción de layouts adaptables a diversas diagonales de pantalla, orientaciones (vertical/horizontal) y tablets con `LayoutBuilder` y `MediaQuery`. |
| `flutter-fix-layout-issues` | Diagnóstico y resolución de desbordamientos de pantalla (`RenderFlex overflowed by X pixels`), restricciones intrínsecas y problemas de scroll anidado. |
| `project-ui` | Guía de estilo visual y sistema de diseño propio del proyecto (paleta de colores, tipografía, componentes reutilizables y estados de interacción). |
