# Skill Registry — Registro de Habilidades de Gentle AI

> **Registro canónico de habilidades operativas para agentes de IA.**
> Este archivo indexa las habilidades (*skills*) disponibles en el repositorio para que el agente orquestador pueda asignarlas dinámicamente a sus subagentes.

---

## ⚙️ Mantenimiento y Regeneración

Este archivo se genera y sincroniza mediante la suite de herramientas **Gentle AI**:

- **Comando de refresco**:
  ```bash
  gentle-ai skill-registry refresh
  ```
  Este comando escanea los directorios de habilidades, actualiza la caché local `.atl/.skill-registry.cache.json` (ignorada en Git) y regenera este documento `.atl/skill-registry.md` manteniendo el formato estándar.

- **Persistencia en Git**:
  - Asegúrate de incluir los cambios de este archivo en el control de versiones con:
    ```bash
    git add -u .atl
    ```

---

## 🎯 Protocolo de Uso para el Agente Orquestador

Cuando el agente orquestador planifica una tarea y delega su ejecución en un subagente (Sonnet, Haiku o Flash), **debe declarar explícitamente las habilidades requeridas** en las instrucciones del subagente:

```markdown
## Skills to load before work
- <id-de-la-skill-1>
- <id-de-la-skill-2>
```

El subagente leerá las directrices de dichas habilidades antes de manipular archivos o proponer cambios, garantizando el cumplimiento de los estándares del proyecto.

---

## 📚 Catálogo Base de Habilidades

### Habilidades de Gobernanza y Flujo

| ID de la Skill | Descripción | Contexto Recomendado |
| :--- | :--- | :--- |
| `core/doc-driven` | Obliga a consultar `docs/` como única fuente de verdad y validar contra requisitos funcionales. | Cualquier tarea funcional o de arquitectura. |
| `core/git-conventions` | Define el formato de Conventional Commits y la política estricta de autoría humana sin firmas de IA. | Preparación de commits y verificación de ramas. |
| `core/review-rdd` | Pautas de auditoría estricta de los 6 atributos de calidad antes de cerrar tareas ODD. | Etapas de revisión previa a merge. |

### Habilidades de Especialización Técnica

| ID de la Skill | Descripción | Contexto Recomendado |
| :--- | :--- | :--- |
| `mobile/flutter-offline-first` | Buenas prácticas para arquitectura local-first, persistencia SQLite/Drift y repositorios desacoplados. | Perfil `mobile-flutter-store`. |
| `mobile/clean-architecture` | Separación estricta en capas (Domain, Data, Presentation) y gestión reactiva de estado (BLoC / Riverpod). | Perfil `mobile-flutter-store`. |
| `testing/unit-tdd` | Ciclo Red-Green-Refactor: escritura de pruebas unitarias previas al código productivo. | Tareas en `odd/tasks/`. |

---

## 📝 Convención para Añadir Nuevas Skills

Para registrar una nueva habilidad manualmente o preparar su inclusión:
1. Crea la definición de la habilidad bajo la carpeta correspondiente en `.atl/skills/<categoria>/<nombre-skill>.md`.
2. Incluye metadatos claros: nombre, propósito, requisitos previos y reglas prescriptivas.
3. Ejecuta `gentle-ai skill-registry refresh` para indexarla en esta tabla canónica.
