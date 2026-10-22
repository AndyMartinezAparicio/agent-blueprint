# {{NOMBRE_PROYECTO}}

> {{DESCRIPCION_CORTA}}

<!--
INSTRUCCIÓN PARA EL AGENTE DE BOOTSTRAP:
El árbol de directorios que se presente a continuación DEBE ser 100% idéntico y coherente
con la estructura de carpetas definida en docs/arquitectura/overview.md y la estructura real en disco.
Si durante la inicialización se personaliza la ruta o subcarpetas de {{CARPETA_CODIGO}},
actualiza este diagrama para que coincida exactamente con docs/arquitectura/overview.md y el disco.
-->

## Estructura del Proyecto

```text
{{NOMBRE_PROYECTO}}/
├── {{CARPETA_CODIGO}}/        # Código fuente modular de la aplicación
│   ├── presentation/          # UI, pantallas, componentes y estilos
│   ├── application/           # Controladores, casos de uso y estado
│   ├── domain/                # Entidades y contratos de repositorio (puro)
│   ├── infrastructure/        # Implementaciones de datos y plataforma
│   └── shared/                # Constantes y utilidades transversales
├── docs/                      # Única fuente de verdad funcional y técnica
│   ├── arquitectura/          # Visión arquitectónica y ADRs (ADR 0001)
│   ├── guias/                 # Guía de desarrollo y convenciones
│   ├── plan/                  # Roadmap maestro y desglose de fases
│   └── producto/              # Visión del producto y matriz de requisitos
├── design/                    # Guías de diseño, notas de proyecto y tokens
├── .claude/                   # Configuración y skills para agentes de IA
├── AGENTS.md                  # Reglas de conducta, calidad y gobernanza
└── README.md                  # Este archivo
```

## Documentación de Referencia

- **Gobernanza y Reglas de Agentes**: [`AGENTS.md`](AGENTS.md)
- **Guía de Desarrollo Local**: [`docs/guias/desarrollo.md`](docs/guias/desarrollo.md)
- **Arquitectura y Decisiones (ADR)**: [`docs/arquitectura/overview.md`](docs/arquitectura/overview.md)
- **Roadmap y Fases**: [`docs/plan/roadmap.md`](docs/plan/roadmap.md)
- **Diseño Visual**: [`design/DESIGN.md`](design/DESIGN.md)

## Estado del Proyecto

El proyecto se encuentra actualmente en fase de inicialización y fundación documental (Día 0).
Consulte [`docs/plan/roadmap.md`](docs/plan/roadmap.md) y [`docs/plan/fases/fase-01-fundacion.md`](docs/plan/fases/fase-01-fundacion.md) para el detalle de la primera fase de desarrollo.
