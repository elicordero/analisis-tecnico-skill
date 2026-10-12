---
name: manual-usuario
description: Genera y mantiene manuales de usuario en español para aplicaciones web, especialmente Laravel 13 y Livewire 4. Analiza flujos reales, documenta pasos, permisos, validaciones, errores frecuentes y usa capturas reales solo cuando exista un navegador automatizado disponible.
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
5. No intentes evadir autenticación ni controles de acceso. Usa únicamente credenciales de prueba proporcionadas expresamente por el usuario y entornos autorizados.
6. Nunca incluyas contraseñas, tokens, claves API, datos personales reales, expedientes reales ni información confidencial en capturas o manuales. Usa datos ficticios y oculta cualquier dato sensible visible.
7. No ejecutes comandos de instalación ni agregues dependencias sin autorización. No instales Playwright, MCP, Pandoc u otras herramientas por cuenta propia.
8. No afirmes que se tomó una captura si no se generó realmente. Si no hay navegador automatizado disponible, entrega el manual sin capturas y añade una lista de capturas pendientes con instrucciones para obtenerlas.
9. No generes archivos adicionales fuera de la carpeta de salida acordada. Si el usuario no especifica carpeta, utiliza `docs/manual-usuario/`.
10. Antes de documentar, pregunta solo por los datos esenciales que falten: público objetivo, módulo/flujo que se documentará, entorno autorizado y formato final. Si la solicitud ya los aclara, continúa sin preguntas innecesarias.

## Flujo de trabajo

### Fase 1: delimitar el manual

Determina:
- Aplicación y módulo.
- Perfil del lector (por ejemplo, operador, administrador o ciudadano).
- Tareas que debe poder completar.
- Versión o rama documentada, si se conoce.
- Formato solicitado: Markdown, PDF o ambos.
- Si existe una URL de pruebas accesible y un navegador automatizado configurado.

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
2. Navega por el flujo de manera no destructiva.
3. Registra nombres reales de menús, botones, campos y mensajes.
4. Captura pantallas reales en los puntos que ayuden a comprender cada paso.
5. Guarda las imágenes en una carpeta `images/` dentro de la carpeta de salida, con nombres descriptivos, por ejemplo `01-listado-tramites.png`.
6. Revisa que no se vean secretos ni datos personales reales. Si no se pueden ocultar con seguridad, no incluyas la captura.
7. No simules que una operación se completó. Si el flujo requiere guardar, enviar, aprobar, pagar, eliminar o cambiar estados, detente antes de la acción y solicita autorización explícita para probarla.

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
- Las imágenes se referencian con rutas relativas.
- No hay credenciales, secretos ni datos reales sensibles.
- Las secciones pendientes están claramente marcadas.
- El manual no contradice mensajes o validaciones observados.
- No se modificó código de la aplicación ni se ejecutaron acciones destructivas.

## Fase 6: salida

- Guarda el archivo principal como `manual.md` dentro de la carpeta de salida acordada.
- Si hay capturas reales, guárdalas en `images/`.
- Si se solicita PDF y existe una herramienta de conversión ya instalada, genera `manual.pdf` a partir del Markdown y verifica que el archivo exista. No instales herramientas por tu cuenta.
- Si no hay conversor disponible, entrega el Markdown y explica brevemente cómo exportarlo a PDF con la herramienta disponible.
- Para manuales grandes, crea un archivo por módulo únicamente si el usuario lo solicita o aprueba el alcance.
- Al finalizar, informa qué se documentó, qué se verificó visualmente, qué archivos se generaron y qué queda pendiente.

## Invocación

Esta skill se puede invocar desde OpenCode con `/manual-usuario` o mencionando `@manual-usuario`, según la versión y configuración instaladas.

Ejemplos:
- “@manual-usuario documenta el módulo de activos para el perfil de administrador. Genera Markdown y PDF; no modifiques la aplicación.”
- “/manual-usuario crea el manual del flujo de creación de trámites. Usa solo capturas reales del entorno de pruebas.”
- “Actualiza el manual del módulo de inspecciones comparando el código actual con `docs/manual-usuario/manual.md`. Modifica únicamente los archivos del manual.”
