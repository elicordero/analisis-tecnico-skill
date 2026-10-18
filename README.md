# analisis-tecnico

Skill de OpenCode para **análisis técnico e ingeniería inversa** de sistemas **Laravel + Livewire** existentes. Inspecciona el código real y genera documentación arquitectónica y diagramas basados en evidencia.

El objetivo es comprender y documentar el sistema sin modificar su comportamiento.

## Qué hace

- Analiza el repositorio: rutas, componentes Livewire, controladores, middleware, modelos Eloquent, migraciones, servicios, acciones, eventos, listeners, jobs, Policies/Gates y dependencias.
- Reconstruye la estructura, el comportamiento, las relaciones, los procesos y las dependencias a partir del código real.
- Genera los diagramas adecuados al alcance: componentes, clases, entidad-relación, secuencia, actividades, estados, casos de uso y BPMN.
- Distingue **hechos comprobados** de **inferencias** y **elementos no determinados**.
- Usa Mermaid, PlantUML o BPMN 2.0 según el tipo de diagrama y las convenciones del proyecto.
- Contrasta modelos Eloquent con migraciones y documenta las discrepancias.
- Retoma y actualiza documentación arquitectónica existente de forma incremental (solo las partes afectadas).
- Aplica un estilo visual limpio, moderno y consistente a todos los diagramas (tema claro, acentos índigo, tipografía y espaciado uniformes).
- Entrega toda la documentación en dos formatos: fuente (`.md`, `.mmd`, `.puml`) y **DOCX editable** para Word.
- Incrusta cada diagrama renderizado (SVG vectorial) en el DOCX junto con su código fuente, para poder editarlo y volver a renderizarlo.
- Genera todo fuera de la carpeta del proyecto, en una carpeta hermana `analisis-tecnico-<nombre-plataforma>`.
- Nunca modifica código de aplicación, configuración ni base de datos; no ejecuta operaciones destructivas; no expone secretos, tokens ni valores sensibles.

## Cómo funciona

1. **Descubrimiento del repositorio**: identifica versiones de Laravel/PHP/Livewire, estructura de directorios, rutas, componentes, modelos, servicios, eventos, autorización, migraciones y dependencias.
2. **Inventario arquitectónico**: módulos funcionales, clases principales, responsabilidades, relaciones, entidades, procesos y mecanismos de seguridad. Cada hallazgo se clasifica como comprobado, inferido o no determinado.
3. **Análisis Laravel/Livewire**: sigue rutas, componentes, modelos, procesos, seguridad y permisos siguiendo las referencias reales del código.
4. **Generación de diagramas**: crea solo los diagramas que aportan valor al alcance solicitado.
5. **Validación**: comprueba sintaxis, nombres, direcciones de dependencias, cardinalidades y flujos contra el repositorio.
6. **Renderizado y DOCX**: renderiza cada diagrama a SVG con el estilo definido y convierte cada documento Markdown a DOCX editable con Pandoc, incrustando los diagramas y su código fuente.
7. **Almacenamiento**: escribe la documentación en una carpeta hermana fuera del proyecto, `analisis-tecnico-<nombre-plataforma>`, sin mezclarla con el código.

## Diagramas

| Diagrama | Notación sugerida |
|---|---|
| Componentes (mapa general) | Mermaid |
| Clases | PlantUML / Mermaid |
| Entidad-relación | Mermaid (`erDiagram`) |
| Secuencia | Mermaid / PlantUML |
| Actividades | Mermaid |
| Estados | Mermaid / PlantUML |
| Casos de uso | PlantUML |
| BPMN | BPMN 2.0 |

Se generan únicamente los diagramas pertinentes al alcance. No se crean diagramas redundantes ni se fuerzan todos los tipos para todos los módulos.

Todos los diagramas usan un tema visual consistente (config de Mermaid y bloque `<style>` de PlantUML incluidos en la skill), y se renderizan a SVG vectorial para mantener la nitidez dentro del DOCX.

## Estructura

```
.opencode/
└── skills/
    └── analisis-tecnico/
        └── SKILL.md      # instrucciones de la skill
```

## Instalación

La skill se resuelve desde un directorio `skills/`. Elige un ámbito:

### Global (todos tus proyectos)

```powershell
New-Item -ItemType Directory -Force "$HOME\.config\opencode\skills" | Out-Null
Copy-Item ".opencode\skills\analisis-tecnico" "$HOME\.config\opencode\skills\analisis-tecnico" -Recurse -Force
```

### Por proyecto

Clona o copia `.opencode/skills/analisis-tecnico` dentro del `.opencode/skills/` del proyecto destino.

Reinicia OpenCode para que detecte la skill.

## Uso

```
/analisis-tecnico
@analisis-tecnico
```

Ejemplos:

- `@analisis-tecnico analiza técnicamente este sistema Laravel y genera un mapa de su arquitectura actual.`
- `/analisis-tecnico analiza el módulo de gestión de activos, sus componentes Livewire, modelos, servicios y dependencias.`
- `Reconstruye el flujo de creación de un trámite desde la ruta hasta la persistencia y genera un diagrama de secuencia.`
- `Genera el diagrama entidad-relación a partir de las migraciones y contrástalo con las relaciones Eloquent.`
- `Revisa cómo se aplican autenticación, autorización y validaciones en el módulo indicado; documenta evidencias y posibles riesgos.`
- `Compara la documentación arquitectónica con el código actual y actualiza únicamente los diagramas afectados.`

Si la solicitud no especifica alcance, la skill comienza con un inventario de alto nivel y propone un análisis por módulos.

## Salida

La documentación se genera **fuera de la carpeta del proyecto**, en una carpeta hermana llamada `analisis-tecnico-<nombre-plataforma>`:

```text
<directorio-padre>/
├── <nombre-proyecto>/                     # el proyecto analizado
└── analisis-tecnico-<nombre-plataforma>/  # salida de la documentación
    ├── README.md
    ├── README.docx
    ├── system-overview.mmd
    ├── components.mmd
    ├── class-diagram.mmd
    ├── database-erd.mmd
    ├── modules/
    │   └── nombre-modulo/
    │       ├── README.md
    │       ├── README.docx
    │       ├── use-cases.puml
    │       ├── activity.mmd
    │       ├── sequence.mmd
    │       └── states.mmd
    ├── assets/            # SVG renderizados de cada diagrama
    ├── findings.md
    ├── findings.docx
    └── reference.docx     # plantilla de estilos para Word
```

`<nombre-plataforma>` es el nombre de la plataforma o sistema analizado: el que indique la solicitud; si no se indica, el nombre del paquete de `composer.json` o, en su defecto, el de la carpeta raíz del proyecto. Los documentos nunca se escriben dentro del proyecto. Si la carpeta de salida ya existe, se reutiliza y actualiza.

- `README.md` / `README.docx`: arquitectura documentada, alcance, limitaciones y enlaces a los diagramas.
- `findings.md` / `findings.docx`: discrepancias comprobadas, relaciones inferidas, áreas no analizadas y riesgos técnicos.
- `assets/`: SVG vectoriales de cada diagrama, incrustados en el DOCX junto a su código fuente.
- `reference.docx`: plantilla de estilos (fuentes, títulos, márgenes, tablas) usada al convertir a Word.
- Si el proyecto ya tiene documentación arquitectónica, se usa como referencia y se respeta su formato en la carpeta de salida; no se escribe dentro del proyecto.

Cada documento se entrega como fuente (`.md`/`.mmd`/`.puml`) y como DOCX editable. En el DOCX, el texto es editable de forma nativa y cada diagrama incluye su código fuente para poder modificarlo y volver a renderizarlo. No se presenta la imagen del diagrama como un objeto editable de Word.

Solo se crean los archivos pertinentes al alcance solicitado.

## Requisitos

- OpenCode con soporte de skills.
- Herramientas para el entregable: la skill las detecta e instala automáticamente si faltan (informa qué instaló).
  - `pandoc` — conversión Markdown a DOCX.
  - `mmdc` (`@mermaid-js/mermaid-cli`) — renderizado de diagramas Mermaid.
  - `java` + `plantuml.jar` — renderizado de diagramas PlantUML.
- Opcional: `rsvg-convert` o `inkscape` como conversión alternativa de SVG.

Si alguna herramienta no puede instalarse, la skill entrega las fuentes e indica el comando exacto pendiente.

## Licencia

[MIT](./LICENSE) © 2026 Eli Cordero
