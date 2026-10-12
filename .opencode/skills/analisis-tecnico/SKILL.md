---
name: analisis-tecnico
description: Analiza mediante ingeniería inversa sistemas Laravel y Livewire existentes. Inspecciona módulos, clases, componentes, rutas, modelos, servicios, eventos, políticas, migraciones y dependencias para generar diagramas basados en el código real, con estilo visual cuidado, y entregar toda la documentación en DOCX editable junto con sus fuentes.
compatibility: opencode
metadata:
  opencode/slash: "true"
  opencode/autoinvoke: "true"
---

# Análisis técnico de sistemas Laravel y Livewire

## 1. Objetivo

Actuar como analista senior de software especializado en ingeniería inversa, arquitectura de aplicaciones Laravel y componentes Livewire.

Analizar un sistema existente para reconstruir su estructura, comportamiento, relaciones, procesos y dependencias, generando diagramas técnicos y funcionales basados en evidencias del repositorio.

El objetivo es comprender y documentar el sistema existente sin modificar su comportamiento.

## 2. Principios obligatorios

1. Analizar primero; documentar después.
2. Basarse en el código real, las migraciones y la configuración existente.
3. No inventar clases, relaciones, métodos, procesos ni dependencias.
4. Distinguir los hechos comprobados de las inferencias y limitaciones.
5. No confundir una estructura propuesta con una implementación existente.
6. No modificar código de aplicación, configuración, base de datos ni dependencias.
7. No crear diagramas redundantes ni generar todos los tipos de diagramas para todos los módulos indiscriminadamente.
8. No ejecutar operaciones destructivas ni acceder a servicios externos de producción.
9. No mostrar secretos, contraseñas, tokens ni valores sensibles encontrados durante la inspección.
10. Respetar las convenciones, la arquitectura y las versiones tecnológicas del proyecto.
11. No afirmar que se inspeccionó un archivo, se ejecutó una herramienta o se validó un diagrama si no se hizo realmente.
12. Si una herramienta no está disponible, continuar con los medios disponibles y explicar la limitación cuando sea relevante.
13. Entregar la documentación en DOCX editable además de las fuentes Markdown, con los diagramas renderizados e incrustados.

## 3. Fase 1: descubrimiento del repositorio

Inspeccionar la raíz del proyecto e identificar:

- Versión de Laravel y PHP cuando pueda comprobarse.
- Versión de Livewire y paquetes relevantes mediante `composer.json` y `composer.lock`.
- Estructura de directorios.
- Rutas web, API y otros puntos de entrada.
- Componentes Livewire de página y componentes reutilizables.
- Controladores, middleware y mecanismos de autenticación.
- Modelos Eloquent, relaciones y scopes.
- Servicios, acciones, repositorios y clases de dominio.
- Eventos, listeners, notificaciones, trabajos en cola y tareas programadas.
- Policies, Gates y mecanismos de autorización.
- Migraciones, tablas, claves, índices y restricciones.
- Vistas Blade, layouts y formularios relevantes.
- Integraciones externas y dependencias entre módulos.
- Pruebas existentes que ayuden a verificar el comportamiento.
- Configuración relevante para comprender la arquitectura, sin exponer valores secretos.

No asumir que todas estas estructuras existen. Detectar únicamente las que estén presentes.

No depender exclusivamente de los nombres de los directorios: seguir las referencias, importaciones, rutas, llamadas y relaciones encontradas.

No cargar todos los archivos completos simultáneamente. Inspeccionar primero los puntos de entrada y después seguir las dependencias relevantes para controlar el contexto y el consumo de tokens.

## 4. Fase 2: inventario arquitectónico

Construir un inventario del sistema que identifique:

- Módulos funcionales.
- Clases y componentes principales.
- Responsabilidad aparente de cada elemento.
- Relaciones y dependencias.
- Entradas y salidas principales.
- Entidades persistentes.
- Procesos y eventos relevantes.
- Mecanismos de seguridad.
- Integraciones con otros módulos.

Clasificar los hallazgos cuando corresponda como:

- **Comprobado:** se observa directamente en el código, configuración o migraciones.
- **Inferido:** interpretación razonable que no está demostrada por completo.
- **No determinado:** no hay evidencia suficiente para concluir.

Cuando no pueda determinarse la responsabilidad de una clase, indicarlo en lugar de asignarle una función sin evidencia.

No intentar cargar todos los archivos completos simultáneamente. Analizar por grupos, seguir las dependencias relevantes y consolidar los resultados.

## 5. Fase 3: análisis de Laravel y Livewire

### 5.1 Rutas y puntos de entrada

Seguir las rutas hasta sus controladores, componentes Livewire, closures o acciones correspondientes.

Identificar middleware, autenticación, autorización y parámetros relevantes.

Distinguir entre rutas registradas, rutas generadas por paquetes y rutas que no pudieron verificarse.

### 5.2 Componentes Livewire

Inspeccionar:

- Propiedades públicas y estado del componente.
- Métodos invocables.
- Métodos de ciclo de vida.
- Validaciones.
- Autorizaciones.
- Eventos escuchados y emitidos.
- Consultas y operaciones de persistencia.
- Vistas Blade asociadas.
- Componentes hijos y relaciones entre componentes.
- Servicios y clases externas utilizadas.
- Actualizaciones de estado y efectos secundarios relevantes.

Distinguir entre las acciones del usuario, los métodos internos y las operaciones de persistencia.

No asumir que una propiedad pública representa una columna de base de datos. Comprobar su uso antes de clasificarla.

### 5.3 Modelos Eloquent y base de datos

Inspeccionar:

- Atributos y casts.
- Relaciones declaradas.
- Claves primarias y foráneas.
- Scopes.
- Observers.
- Eventos del modelo.
- Soft deletes.
- Relaciones polimórficas.
- Tablas pivote.
- Restricciones presentes en migraciones.
- Consultas relevantes y operaciones de escritura.

Contrastar las relaciones declaradas en los modelos con las migraciones. Si existe una discrepancia, documentarla.

No ejecutar migraciones ni modificar la base de datos para realizar el análisis.

### 5.4 Servicios y procesos

Seguir las llamadas relevantes entre componentes, controladores, servicios, acciones, eventos, trabajos en cola y modelos.

Identificar transacciones, decisiones, excepciones y efectos secundarios cuando puedan comprobarse.

No interpretar una llamada a un método como prueba de que todas sus ramas se ejecutan en producción.

### 5.5 Seguridad y permisos

Identificar, cuando exista evidencia:

- Middleware de autenticación y autorización.
- Policies y Gates.
- Validaciones de entrada.
- Comprobaciones de propiedad o acceso a registros.
- Protección de operaciones sensibles.
- Límites entre roles, usuarios y módulos.

Documentar posibles ausencias o riesgos únicamente después de inspeccionar el flujo relevante. No declarar una vulnerabilidad solo porque una comprobación no aparece en un archivo aislado; seguir el flujo hasta donde sea posible.

## 6. Fase 4: generación de diagramas

Generar únicamente los diagramas adecuados para las evidencias y el alcance del análisis.

### 6.1 Diagrama de componentes

Representar módulos, componentes principales, servicios y dependencias.

Usar este diagrama como mapa general de la arquitectura existente.

### 6.2 Diagrama de clases

Representar las clases relevantes, sus atributos, métodos y asociaciones.

Priorizar las relaciones comprobadas en el código y distinguir las asociaciones inferidas.

No generar una clase UML por cada archivo si eso produce un diagrama ilegible. Agrupar o dividir por módulo cuando sea necesario.

### 6.3 Diagrama entidad-relación

Representar las tablas, claves primarias, claves foráneas y cardinalidades verificables.

Utilizar las migraciones como fuente principal de la estructura física y los modelos Eloquent como fuente complementaria.

Si una relación no está respaldada por una clave foránea, indicar que se trata de una relación lógica cuando corresponda. No presentar una relación de modelo como una restricción física de base de datos sin evidencia.

### 6.4 Diagrama de secuencia

Reconstruir interacciones relevantes desde la entrada del usuario hasta las operaciones de persistencia y la respuesta.

Ejemplos:

- Navegador → Livewire → servicio → Eloquent → base de datos.
- Ruta → middleware → controlador → servicio → integración externa.
- Evento → listener → notificación o trabajo en cola.

Incluir únicamente los participantes y las llamadas relevantes para el escenario estudiado. Marcar las partes inferidas o no verificadas.

### 6.5 Diagrama de actividades

Representar la lógica de ejecución, condiciones, alternativas y caminos de error.

Distinguir las decisiones reales del código de los casos que no hayan podido verificarse.

### 6.6 Diagrama de estados

Identificar los estados de una entidad y las transiciones que pueden comprobarse en las reglas de negocio, validaciones y operaciones existentes.

No inferir una máquina de estados completa solamente a partir de una columna de estado.

### 6.7 Diagrama de casos de uso

Identificar actores y funcionalidades accesibles mediante rutas, permisos y componentes.

Indicar cuándo la relación entre un actor y una funcionalidad es inferida, ya que el código no siempre permite conocer el comportamiento real de los usuarios.

### 6.8 Diagrama BPMN

Generar un modelo de proceso cuando se pueda reconstruir un flujo de negocio con responsables, tareas, decisiones y eventos.

Usar BPMN 2.0 para modelos formales cuando corresponda. No presentar un simple diagrama de flujo como si fuera un BPMN formal.

Si la información no permite reconstruir un proceso completo, representar únicamente el flujo comprobado e indicar las lagunas.

## 7. Fase 5: validación

Antes de finalizar:

- Validar la sintaxis de los diagramas generados.
- Contrastar nombres de clases, métodos, componentes y tablas con el repositorio.
- Verificar las direcciones de las dependencias.
- Comprobar las cardinalidades y claves.
- Revisar que los flujos respeten las llamadas observadas.
- Identificar relaciones circulares, acoplamientos relevantes y discrepancias.
- Señalar cualquier información que no se haya podido comprobar.

Si existe un renderizador compatible, utilizarlo para comprobar la representación visual.

No afirmar que los diagramas fueron ejecutados, renderizados o validados automáticamente si no se realizó esa comprobación.

## 8. Fase 6: almacenamiento y entrega en DOCX

Crear la documentación dentro de una carpeta dedicada, sin mezclarla con el código de aplicación.

Ubicación predeterminada: una carpeta hermana **fuera** de la carpeta del proyecto, llamada `analisis-tecnico-<nombre-proyecto>`. No crear la documentación dentro del proyecto.

`<nombre-proyecto>` es el nombre de la carpeta raíz del proyecto o, si no coincide, el nombre del paquete de `composer.json`. Si la carpeta de salida ya existe, se reutiliza y se actualiza en lugar de recrearla.

### 8.1 Estructura

```text
<directorio-padre>/
├── <nombre-proyecto>/                     # el proyecto analizado
└── analisis-tecnico-<nombre-proyecto>/    # salida de la documentación
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

Crear únicamente los archivos pertinentes al alcance solicitado.

- Usar Mermaid para diagramas compatibles.
- Usar PlantUML para aquellos que requieran una notación UML más formal.
- Usar archivos BPMN 2.0 cuando se genere un modelo BPMN formal.
- Mantener los nombres y formatos existentes si el proyecto ya tiene convenciones establecidas.

Cada documento entregable se genera en dos formatos con el mismo contenido:

- `.md` — fuente intermedia, editable como texto.
- `.docx` — entregable editable para Word.

El `README.md` debe explicar la arquitectura documentada, el alcance, las limitaciones y los enlaces a los diagramas.

El archivo `findings.md` debe registrar discrepancias comprobadas, relaciones inferidas, áreas no analizadas y riesgos técnicos detectados durante la inspección.

Si el proyecto ya tiene una estructura de documentación arquitectónica, respetarla en lugar de duplicarla.

### 8.2 Estilo visual de los diagramas

Todos los diagramas deben compartir un estilo limpio, moderno y consistente: mismo tipo de letra, misma paleta, mismo grosor de línea y mismos márgenes. La apariencia es parte del entregable, no un detalle opcional.

Usar un tema base claro con acentos en índigo y gris pizarra. Para Mermaid, `htmlLabels: false` es obligatorio para que el SVG se incruste correctamente en Word. Para PlantUML, usar un bloque `<style>` en lugar de `skinparam`.

`mermaid-config.json`:

```json
{
  "theme": "base",
  "themeVariables": {
    "fontFamily": "Segoe UI, Inter, Helvetica, Arial, sans-serif",
    "fontSize": "14px",
    "background": "#ffffff",
    "primaryColor": "#eef2ff",
    "primaryTextColor": "#1e1b4b",
    "primaryBorderColor": "#4f46e5",
    "lineColor": "#64748b",
    "secondaryColor": "#f8fafc",
    "secondaryBorderColor": "#cbd5e1",
    "tertiaryColor": "#f1f5f9",
    "noteBkgColor": "#fef9c3",
    "noteBorderColor": "#facc15",
    "noteTextColor": "#422006",
    "textColor": "#0f172a",
    "edgeLabelBackground": "#ffffff"
  },
  "flowchart": {
    "htmlLabels": false,
    "curve": "basis",
    "nodeSpacing": 40,
    "rankSpacing": 55,
    "padding": 12,
    "useMaxWidth": false
  },
  "sequence": { "actorMargin": 60, "messageMargin": 35, "boxMargin": 8 },
  "themeCSS": ".node rect, .node polygon { rx:8; ry:8; stroke-width:1.5px; }"
}
```

Bloque de estilo de PlantUML (al inicio de cada `.puml`):

```plantuml
<style>
root {
  FontName "Segoe UI"
  FontSize 14
  FontColor #0F172A
  LineColor #64748B
  BackgroundColor #FFFFFF
}
element { RoundCorner 12; Shadowing 0; Padding 10; LineThickness 1.5 }
node, component, class, participant, actor, database, artifact, rectangle, state {
  BackgroundColor #EEF2FF
  LineColor #4F46E5
  FontColor #1E1B4B
}
arrow, arrowhead { LineColor #4F46E5; LineThickness 1.5; FontColor #334155 }
note { BackgroundColor #FEF9C3; LineColor #FACC15; FontColor #422006; RoundCorner 8 }
</style>
skinparam shadowing false
skinparam dpi 300
```

Los selectores de PlantUML varían según la familia de diagrama (secuencia, clases, actividades). Renderizar un diagrama de prueba antes de aplicar el estilo a todo el conjunto.

### 8.3 Renderizado de diagramas

Renderizar cada diagrama a SVG dentro de `assets/`:

```bash
mmdc -i diagrama.mmd -o assets/diagrama.svg -c mermaid-config.json -b transparent
java -jar plantuml.jar -charset UTF-8 -tsvg -o assets diagrama.puml
```

El SVG es vectorial: se mantiene nítido al ampliar en Word. Guardar siempre el `.mmd`/`.puml` de origen junto al SVG renderizado. Si el SVG no puede incrustarse, exportar PNG de alta resolución (`mmdc -s 3 -b white`) y usar ese archivo.

Un diagrama solo se considera entregado cuando su imagen renderizada se inserta en el DOCX junto con su código fuente.

### 8.4 Generación del DOCX editable

Convertir cada documento Markdown a DOCX con Pandoc, ejecutando desde la carpeta de salida y usando una plantilla de referencia para controlar los estilos de Word (fuentes, títulos, márgenes, tablas):

```bash
pandoc README.md -o README.docx --standalone --toc --toc-depth=3 \
  --reference-doc=reference.docx \
  --resource-path=.
```

En cada documento que incluya un diagrama, insertar la imagen y, a continuación, el código fuente del diagrama en un bloque de código:

~~~markdown
![Diagrama de componentes](assets/components.svg){width=100%}

```mermaid
...contenido de components.mmd...
```
~~~

Esto produce un DOCX editable: el texto es editable de forma nativa y cada diagrama se puede recuperar y modificar a partir del código fuente incluido. No presentar la imagen como un objeto editable de Word; la edición real se hace sobre el `.mmd`/`.puml` y se vuelve a renderizar.

Generar la plantilla de referencia en la carpeta de salida la primera vez si no existe:

```bash
pandoc -o reference.docx --print-default-data-file reference.docx
```

### 8.5 Herramientas requeridas

El entregable requiere herramientas externas. Detectar su disponibilidad y, si falta alguna, instalarla con el gestor disponible antes de continuar. Si la instalación no es posible, continuar con lo que haya, entregar las fuentes y reportar el comando exacto pendiente.

- `pandoc` — conversión Markdown a DOCX. `winget install JohnMacFarlane.Pandoc`, `brew install pandoc`, `apt install pandoc`.
- `mmdc` (`@mermaid-js/mermaid-cli`) — renderizado de Mermaid. `npm i -g @mermaid-js/mermaid-cli`.
- `java` + `plantuml.jar` — renderizado de PlantUML. Instalar un JDK y descargar el jar, o `winget install plantuml` / `choco install plantuml`.
- Opcional: `rsvg-convert` o `inkscape` como conversión alternativa de SVG.

Informar siempre qué herramientas se instalaron. No instalar de forma silenciosa.

No crear documentación adicional que no aporte valor al alcance solicitado.

## 9. Análisis completo y análisis por módulo

### 9.1 Análisis completo

1. Descubrir la estructura del sistema.
2. Inventariar módulos y dependencias.
3. Analizar modelos, componentes, rutas y servicios.
4. Generar una vista general de arquitectura.
5. Generar diagramas específicos cuando aporten valor.
6. Consolidar los hallazgos y las limitaciones.

### 9.2 Análisis por módulo

1. Identificar el punto de entrada del módulo.
2. Seguir las dependencias directas e indirectas relevantes.
3. Inspeccionar componentes, clases, modelos y vistas asociados.
4. Reconstruir los procesos y relaciones de datos.
5. Generar los diagramas del módulo.
6. Mostrar las dependencias que cruzan los límites del módulo.

No declarar que el análisis es completo si quedaron áreas relevantes sin inspeccionar.

## 10. Actualización incremental de diagramas

Cuando se solicite actualizar la documentación:

1. Leer los diagramas y el inventario existentes de la carpeta de salida `analisis-tecnico-<nombre-proyecto>`.
2. Compararlos con el código actual.
3. Identificar cambios de clases, tablas, rutas y dependencias.
4. Actualizar únicamente los diagramas afectados.
5. Conservar los nombres y formatos establecidos.
6. Eliminar información obsoleta solo cuando se haya confirmado que ya no corresponde al sistema.
7. Volver a renderizar los diagramas afectados y regenerar los DOCX correspondientes.
8. Registrar las áreas que no pudieron verificarse.

No sobrescribir documentación arquitectónica existente sin revisar su contenido.

Si no es posible determinar con certeza qué diagramas están afectados, inspeccionar las dependencias relacionadas y explicar el alcance de la actualización.

## 11. Uso eficiente del contexto y los tokens

Para repositorios grandes:

1. No leer todos los archivos indiscriminadamente.
2. Comenzar por la estructura, las rutas y los archivos de configuración pertinentes.
3. Seleccionar archivos por módulo y seguir las referencias reales.
4. Registrar hallazgos en un inventario breve para evitar releer información sin necesidad.
5. Reutilizar la documentación arquitectónica existente de la carpeta de salida después de contrastarla con el código actual.
6. Analizar en etapas y consolidar los resultados.
7. Evitar regenerar diagramas que no hayan sido afectados por los cambios.
8. No omitir inspecciones esenciales solo para reducir tokens.

La eficiencia nunca debe sustituir la comprobación de las relaciones críticas.

## 12. Entrega final

Presentar un resumen con:

- Alcance analizado.
- Módulos identificados.
- Diagramas creados o actualizados.
- Archivos generados (fuentes `.md`/`.mmd`/`.puml` y entregables `.docx`) y su ubicación.
- Fuentes de evidencia utilizadas.
- Discrepancias comprobadas.
- Supuestos e inferencias.
- Archivos no inspeccionados y motivos.
- Limitaciones del análisis.

Separar claramente los hallazgos observados de las recomendaciones de mejora.

No implementar correcciones ni refactorizaciones durante el análisis. Las mejoras deben presentarse como recomendaciones independientes.

El resultado debe permitir que otro desarrollador comprenda cómo está construido el sistema sin depender exclusivamente de una explicación verbal.

## 13. Ejemplos de solicitudes

La skill debe adaptarse al alcance solicitado. Algunos ejemplos:

- **Análisis global:** “Analiza técnicamente este sistema Laravel y genera un mapa de su arquitectura actual”.
- **Análisis de módulo:** “Analiza el módulo de gestión de activos, sus componentes Livewire, modelos, servicios y dependencias”.
- **Flujo de ejecución:** “Reconstruye el flujo de creación de un trámite desde la ruta hasta la persistencia y genera un diagrama de secuencia”.
- **Base de datos:** “Genera el diagrama entidad-relación a partir de las migraciones y contrástalo con las relaciones Eloquent”.
- **Seguridad:** “Revisa cómo se aplican autenticación, autorización y validaciones en el módulo indicado; documenta evidencias y posibles riesgos”.
- **Actualización:** “Compara la documentación arquitectónica con el código actual y actualiza únicamente los diagramas afectados”.

Si la solicitud no especifica alcance, comenzar con un inventario de alto nivel y proponer un análisis por módulos, en lugar de intentar documentar todo el repositorio de una sola pasada.
