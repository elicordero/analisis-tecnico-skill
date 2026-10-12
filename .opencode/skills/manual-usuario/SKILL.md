---
name: manual-usuario
description: Genera y mantiene manuales de usuario en español para aplicaciones web, especialmente Laravel 13 y Livewire 4. Solicita datos de login cuando el flujo requiere autenticación, analiza flujos reales, documenta pasos, permisos, validaciones, errores frecuentes y usa capturas reales solo cuando exista un navegador automatizado disponible. Guarda la salida fuera del proyecto, en la carpeta manual-usuario-<nombre-proyecto>, y entrega el resultado en formato DOCX.
compatibility: opencode
metadata:
  audience: documentation
  workflow: user-manuals
  opencode/slash: "true"
  opencode/autoinvoke: "false"
---

# Skill: Manuales de usuario

## Objetivo

Crear manuales funcionales, precisos y mantenibles para usuarios finales. Prioriza lo que una persona necesita hacer en la interfaz, no una explicación del código fuente. El idioma predeterminado es español claro, formal y neutral.

Esta skill es bajo demanda. No generes ni actualices documentación durante tareas normales de desarrollo si el usuario no lo solicita.

## Reglas obligatorias

1. Inspecciona el proyecto antes de documentarlo. Identifica framework, rutas, componentes de página, vistas, formularios, permisos y flujos relacionados.
2. Documenta únicamente funciones que puedas confirmar en el código o verificar en una aplicación accesible. No inventes botones, campos, permisos, mensajes ni resultados.
3. Distingue entre comportamiento confirmado por código y comportamiento comprobado visualmente. Si algo no se puede confirmar, indícalo como pendiente de validación.
4. No modifiques código de la aplicación, datos, configuración ni permisos para producir el manual. No envíes formularios reales, no borres ni crees registros y no ejecutes acciones destructivas.
5. No intentes evadir autenticación ni controles de acceso. Cuando el flujo requiera iniciar sesión, pide siempre al usuario los datos de login (URL de acceso, usuario y contraseña de prueba) antes de continuar, y espera a recibirlos. Usa únicamente credenciales de prueba proporcionadas expresamente por el usuario y entornos autorizados. Nunca inventes credenciales, nunca las guardes en archivos y nunca las incluyas en el manual.
6. Nunca incluyas contraseñas, tokens, claves API, datos personales reales, expedientes reales ni información confidencial en capturas o manuales. Usa datos ficticios y oculta cualquier dato sensible visible.
7. No ejecutes comandos de instalación ni agregues dependencias sin autorización. No instales Playwright, MCP, Pandoc u otras herramientas por cuenta propia.
8. No afirmes que se tomó una captura si no se generó realmente. Si no hay navegador automatizado disponible, entrega el manual sin capturas y añade una lista de capturas pendientes con instrucciones para obtenerlas.
9. Genera el manual fuera de la ruta del proyecto, nunca dentro de su árbol de directorios. Usa como carpeta de salida `manual-usuario-<nombre-proyecto>`, ubicada como hermana del directorio raíz del proyecto (por ejemplo, `..\manual-usuario-<nombre-proyecto>` en Windows o `../manual-usuario-<nombre-proyecto>` en Linux/macOS). `<nombre-proyecto>` es el nombre de la carpeta raíz del proyecto o, si existe, el nombre del paquete de `composer.json`. Si el usuario indica otra carpeta, respétala siempre que esté fuera del proyecto. No generes archivos adicionales fuera de esa carpeta.
10. Antes de documentar, pregunta solo por los datos esenciales que falten: público objetivo, módulo/flujo que se documentará, entorno autorizado, datos de login (si el flujo requiere autenticación), formato final y carpeta de salida (solo si el usuario quiere una distinta a la predeterminada). Si la solicitud ya los aclara, continúa sin preguntas innecesarias.

## Flujo de trabajo

### Fase 1: delimitar el manual

Determina:
- Aplicación y módulo.
- Perfil del lector (por ejemplo, operador, administrador o ciudadano).
- Tareas que debe poder completar.
- Versión o rama documentada, si se conoce.
- Formato de salida: **DOCX** (obligatorio). Conserva el Markdown como fuente intermedia para generar el DOCX.
- Si existe una URL de pruebas accesible y un navegador automatizado configurado.
- Si el flujo requiere autenticación, solicita los datos de login de prueba (URL, usuario y contraseña) antes de avanzar.
- Carpeta de salida. Por defecto `manual-usuario-<nombre-proyecto>`, hermana del proyecto y fuera de su árbol. Confírmala si el usuario no la indicó.

Si el usuario pide un manual completo, primero inventaría los módulos detectables y presenta una propuesta de alcance antes de intentar cubrir toda la aplicación.

### Fase 2: inspeccionar el código

Para proyectos Laravel 13 + Livewire 4, revisa según corresponda:
- `routes/web.php` y archivos de rutas adicionales.
- Componentes Livewire en `app/Livewire/` y sus vistas asociadas.
- Vistas Blade en `resources/views/`.
- Middleware, Policies, Gates y comprobaciones de autorización.
- Requests, reglas de validación y mensajes visibles al usuario.
- Menús, navegación, layouts, formularios, tablas, modales y estados vacíos.
- Traducciones y mensajes de éxito/error.
- Tests existentes solo como fuente complementaria de comportamiento; no crees ni modifiques pruebas.

Usa búsquedas dirigidas y lee solo los archivos relevantes. No asumas que el nombre de una clase describe exactamente el comportamiento visible.

### Fase 3: verificar el flujo visual

Si el usuario proporciona una URL de un entorno de pruebas y existe Playwright MCP u otra herramienta de navegador ya configurada:
1. Confirma que el entorno es autorizado y no productivo, salvo autorización explícita.
2. Si el flujo requiere iniciar sesión, pide los datos de login al usuario y espera a recibirlos antes de navegar. Usa solo credenciales de prueba; nunca credenciales de producción y nunca las guardes en archivos.
3. Navega por el flujo de manera no destructiva.
4. Registra nombres reales de menús, botones, campos y mensajes.
5. Captura pantallas reales en los puntos que ayuden a comprender cada paso.
6. Guarda las imágenes en una carpeta `images/` dentro de la carpeta de salida, con nombres descriptivos, por ejemplo `01-listado-tramites.png`.
7. Revisa que no se vean secretos ni datos personales reales. Si no se pueden ocultar con seguridad, no incluyas la captura.
8. No simules que una operación se completó. Si el flujo requiere guardar, enviar, aprobar, pagar, eliminar o cambiar estados, detente antes de la acción y solicita autorización explícita para probarla.

Si el navegador no está disponible, no instales ni configures nada automáticamente. Continúa mediante análisis de código y enumera las capturas que el usuario debe proporcionar o habilitar.

### Fase 4: redactar el manual

Usa esta estructura, adaptándola al tamaño del módulo:

# Manual de usuario: [nombre del módulo]

- Aplicación:
- Módulo:
- Público objetivo:
- Versión/fecha de revisión:
- Estado de verificación: código revisado / interfaz verificada / parcialmente verificado

## 1. Objetivo
Explica en lenguaje sencillo para qué sirve el módulo.

## 2. Requisitos de acceso
Indica el rol o permiso necesario solo si se ha confirmado. No incluyas credenciales.

## 3. Cómo ingresar
Describe la navegación desde el menú real de la aplicación.

## 4. Procedimientos
Para cada tarea:
1. Propósito.
2. Pasos numerados y concretos.
3. Campos requeridos y formato esperado.
4. Validaciones y mensajes que se hayan confirmado.
5. Resultado esperado.
6. Captura real, si existe, con texto alternativo y referencia dentro del paso.

## 5. Estados, permisos y restricciones
Explica qué puede hacer cada perfil únicamente cuando esté respaldado por evidencia.

## 6. Errores frecuentes y solución
Incluye solo errores confirmados. Para problemas no verificados, etiquétalos como posibles y explica cómo confirmarlos.

## 7. Preguntas frecuentes
Incluye preguntas prácticas derivadas del flujo documentado.

## 8. Glosario
Define términos técnicos necesarios para el usuario final.

## 9. Pendientes de verificación
Lista explícitamente las dudas, pantallas inaccesibles o pasos no verificados.

## Reglas de redacción

- Escribe en español claro, formal y orientado a tareas.
- Dirígete al usuario de forma consistente; prefiere instrucciones directas: “Seleccione”, “Ingrese”, “Presione”.
- Una acción por paso. Mantén los pasos cortos.
- Usa los nombres exactos de la interfaz, entre comillas cuando sea útil.
- No expliques clases, métodos, tablas o arquitectura salvo que el público sea técnico y lo solicite.
- No uses capturas decorativas ni ilustraciones inventadas como si fueran la interfaz real.
- Numera las capturas en orden de aparición y añade una leyenda breve.
- No expongas rutas internas, nombres de servidores, IP, stack traces ni detalles sensibles.
- Incluye fecha de revisión, alcance y limitaciones.

## Fase 5: revisar calidad

Antes de entregar, verifica:
- Cada procedimiento corresponde a una función existente.
- Los pasos siguen el orden real de la interfaz.
- Los campos y permisos no fueron inferidos sin evidencia.
- Las capturas existen, corresponden a la versión documentada y no contienen información sensible.
- Las imágenes quedan embebidas en el DOCX o referenciadas con rutas relativas en el Markdown.
- El archivo `manual.docx` se generó y no está vacío.
- No hay credenciales, secretos ni datos reales sensibles.
- Las secciones pendientes están claramente marcadas.
- El manual no contradice mensajes o validaciones observados.
- No se modificó código de la aplicación ni se ejecutaron acciones destructivas.
- La salida está fuera de la ruta del proyecto, en la carpeta `manual-usuario-<nombre-proyecto>`.
- Solo se usaron credenciales de prueba solicitadas al usuario y ninguna quedó guardada en el manual ni en otros archivos.

## Fase 6: salida

- Genera el archivo final `manual.docx` en la carpeta de salida. El DOCX es el entregable obligatorio. Mantén la salida fuera de la ruta del proyecto (carpeta por defecto `manual-usuario-<nombre-proyecto>`, hermana del directorio raíz). Nunca escribas la salida dentro del proyecto.
- Conserva el `manual.md` fuente en la misma carpeta de salida.
- Si hay capturas reales, guárdalas en `images/` dentro de esa carpeta e insértalas en el DOCX, numeradas y con leyenda breve.
- Convierte el Markdown a DOCX con una herramienta ya instalada (por ejemplo `pandoc manual.md -o manual.docx` o `libreoffice --headless --convert-to docx manual.md`). Verifica que `manual.docx` exista y no esté vacío. No instales herramientas por tu cuenta.
- Si no hay conversor disponible, entrega `manual.md`, indica que falta la conversión a DOCX e incluye el comando exacto para generarlo con la herramienta disponible.
- Para manuales grandes, crea un archivo por módulo únicamente si el usuario lo solicita o aprueba el alcance.
- Al finalizar, informa qué se documentó, qué se verificó visualmente, qué archivos se generaron (con la ruta completa de la carpeta de salida) y qué queda pendiente.

## Invocación

Esta skill se puede invocar desde OpenCode con `/manual-usuario` o mencionando `@manual-usuario`, según la versión y configuración instaladas.

Ejemplos:
- “@manual-usuario documenta el módulo de activos para el perfil de administrador. Genera el DOCX; no modifiques la aplicación.”
- “/manual-usuario crea el manual del flujo de creación de trámites. Usa solo capturas reales del entorno de pruebas.”
- “Actualiza el manual del módulo de inspecciones comparando el código actual con `../manual-usuario-<nombre-proyecto>/manual.md`. Modifica únicamente los archivos del manual.”
