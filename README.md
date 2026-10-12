# manual-usuario

Skill de OpenCode para generar y mantener manuales de usuario en español, orientados a tareas y basados en evidencia. Pensada para aplicaciones web, en especial **Laravel 13 + Livewire 4**.

## Qué hace

- Inspecciona rutas, componentes Livewire, vistas Blade, permisos (Policies/Gates), validaciones y traducciones antes de documentar.
- Documenta únicamente funciones confirmadas en código o verificadas en una interfaz accesible.
- Verifica flujos visuales con navegador automatizado solo si ya está configurado (Playwright MCP u otro); usa capturas reales, nunca inventadas.
- Nunca modifica el código de la aplicación, ni ejecuta acciones destructivas, ni incluye credenciales, secretos o datos personales reales.
- Entrega el manual en Markdown y, si hay conversor disponible, en PDF.

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

- `@manual-usuario documenta el módulo de activos para el perfil de administrador. Genera Markdown y PDF; no modifiques la aplicación.`
- `/manual-usuario crea el manual del flujo de creación de trámites. Usa solo capturas reales del entorno de pruebas.`
- `Actualiza el manual del módulo de inspecciones comparando el código actual con docs/manual-usuario/manual.md.`

Salida por defecto en `docs/manual-usuario/`:

```
docs/manual-usuario/
├── manual.md
├── manual.pdf        # si hay conversor disponible
└── images/           # capturas reales
```

## Requisitos

- OpenCode con soporte de skills.
- Opcional: navegador automatizado (Playwright MCP u otro) para verificación visual y capturas.
- Opcional: conversor Markdown a PDF ya instalado (Pandoc u otro). La skill no instala herramientas por su cuenta.

## Licencia

[MIT](./LICENSE)
