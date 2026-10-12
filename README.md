# manual-usuario

Skill de OpenCode para generar y mantener manuales de usuario en español, orientados a tareas y basados en evidencia. Pensada para aplicaciones web, en especial **Laravel 13 + Livewire 4**.

## Qué hace

- Inspecciona rutas, componentes Livewire, vistas Blade, permisos (Policies/Gates), validaciones y traducciones antes de documentar.
- Documenta únicamente funciones confirmadas en código o verificadas en una interfaz accesible.
- Verifica flujos visuales con navegador automatizado solo si ya está configurado (Playwright MCP u otro); usa capturas reales, nunca inventadas.
- Nunca modifica el código de la aplicación, ni ejecuta acciones destructivas, ni incluye credenciales, secretos o datos personales reales.
- Solicita los datos de login de prueba (URL, usuario y contraseña) cuando el flujo requiere autenticación, y nunca los guarda ni los incluye en el manual.
- Genera la salida **fuera del proyecto**, en una carpeta hermana llamada `manual-usuario-<nombre-proyecto>`.
- Entrega el manual final en **DOCX** (`manual.docx`), usando Markdown como fuente intermedia.

Es una skill **bajo demanda**: no se activa durante el trabajo normal de desarrollo.

## Estructura

```
.opencode/
└── skills/
    └── manual-usuario/
        └── SKILL.md      # instrucciones de la skill
```

## Instalación

La skill se resuelve desde un directorio `skills/`. Elige un ámbito:

### Global (todos tus proyectos)

```powershell
New-Item -ItemType Directory -Force "$HOME\.config\opencode\skills" | Out-Null
Copy-Item ".opencode\skills\manual-usuario" "$HOME\.config\opencode\skills\manual-usuario" -Recurse -Force
```

### Por proyecto

Clona o copia `.opencode/skills/manual-usuario` dentro del `.opencode/skills/` del proyecto destino.

Reinicia OpenCode para que detecte la skill.

## Uso

```
/manual-usuario
@manual-usuario
```

Ejemplos:

- `@manual-usuario documenta el módulo de activos para el perfil de administrador. Genera el DOCX; no modifiques la aplicación.`
- `/manual-usuario crea el manual del flujo de creación de trámites. Usa solo capturas reales del entorno de pruebas.`
- `Actualiza el manual del módulo de inspecciones comparando el código actual con ../manual-usuario-mi-proyecto/manual.md.`

Salida por defecto **fuera de la ruta del proyecto**, en una carpeta hermana llamada `manual-usuario-<nombre-proyecto>`:

```
<directorio-padre>/
├── mi-proyecto/                # el proyecto
└── manual-usuario-mi-proyecto/ # salida del manual
    ├── manual.md               # fuente Markdown (intermedia)
    ├── manual.docx             # entregable final (obligatorio)
    └── images/                 # capturas reales embebidas en el DOCX
```

`<nombre-proyecto>` es el nombre de la carpeta raíz del proyecto o el nombre del paquete de `composer.json`.

## Requisitos

- OpenCode con soporte de skills.
- Opcional: navegador automatizado (Playwright MCP u otro) para verificación visual y capturas.
- Necesario para el entregable: conversor de Markdown a DOCX ya instalado (Pandoc, LibreOffice u otro). La skill no instala herramientas por su cuenta.

## Licencia

[MIT](./LICENSE)
