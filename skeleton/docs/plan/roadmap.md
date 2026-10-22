# Roadmap de {{NOMBRE_PROYECTO}}

> **Fuente Canónica de Estado de Fases:**
> Este documento es el **único lugar** donde vive el estado oficial de cada fase del proyecto (*Pendiente*, *En curso*, *Aprobada*). Ningún otro archivo debe duplicar ni contradecir esta información.

---

## 1. Tabla Maestra de Fases

| Fase | Título | Versión | Estado | Documento de Fase |
|:---:|:---|:---:|:---:|:---|
| **01** | Base, tema y datos de prueba | `v0.1.0` | **Pendiente** | [fase-01-fundacion.md](fases/fase-01-fundacion.md) |
| **02** | {{TITULO_FASE_02}} | `v0.2.0` | **Pendiente** | `fase-02-{{SLUG_02}}.md` |
| **03** | {{TITULO_FASE_03}} | `v0.3.0` | **Pendiente** | `fase-03-{{SLUG_03}}.md` |
| **04** | {{TITULO_FASE_04}} | `v0.4.0` | **Pendiente** | `fase-04-{{SLUG_04}}.md` |
| **05** | Pulido final y preparación de lanzamiento | `v1.0.0` | **Pendiente** | `fase-05-lanzamiento-v1.md` |

*Estados posibles:*
- ⚪ `Pendiente`: Fase planificada, aún no iniciada.
- 🟡 `En curso`: Fase activa en desarrollo. Solo debe haber **una** fase en curso a la vez.
- 🟢 `Aprobada`: Todos los criterios de aceptación han sido cumplidos y verificados con éxito.

---

## 2. Regla de Cierre de Fase

Cuando una fase alcanza todos sus criterios de aceptación y se valida mediante prueba real del usuario:

1. **Revisión de Calidad:**
   - Linter y análisis estático limpios al 100% (cero advertencias, cero errores).
   - Suite completa de tests automáticos en verde.
2. **Actualización Documental:**
   - En este documento (`roadmap.md`), marcar la fase como **Aprobada**.
   - En [`docs/CHANGELOG.md`](../CHANGELOG.md), transferir las novedades de `## [Sin publicar]` a la sección `## [X.Y.Z] - AAAA-MM-DD`.
3. **Flujo de Git y Tagging:**
   - La rama de la fase (`feature/fase-XX-*`) se fusiona en `develop`.
   - `develop` se fusiona en `main`.
   - Se crea y publica el tag anotado en `main`: `git tag -a vX.Y.Z -m "Release vX.Y.Z - Fase XX"`.
   - Se empuja a remoto: `git push origin main --tags` y `git push origin develop`.
