# Plugin EyeQuant para Claude Code

Este plugin conecta Claude Code con el MCP remoto de EyeQuant y añade una habilidad para consultar señales, historial, perfil y watchlists. El servidor y sus herramientas están en `https://www.eyequant.ai/mcp`; no hay procesos locales ni claves dentro del plugin.

## Probar el plugin localmente

Desde la raíz del repositorio `eyequant-plugin-claude`, inicia Claude Code con:

```sh
claude --plugin-dir .
```

Mientras el plugin siga en `plugins/eyequant` dentro del repositorio de la aplicación, usa `claude --plugin-dir ./plugins/eyequant` desde la raíz de ese repositorio.

Dentro de Claude Code, ejecuta `/mcp` y completa el inicio de sesión OAuth de EyeQuant cuando se solicite. El plugin solicita `eyequant:read` y `eyequant:watchlist.write`; los cambios de watchlists también requieren un plan que permita la operación. La habilidad queda disponible como `/eyequant:eyequant` y Claude puede activarla según la consulta. El servidor EyeQuant debe tener desplegado el cambio OAuth que acepta la URL local de retorno de Claude Code.

## Instalar desde GitHub

```sh
claude plugin marketplace add cristaros/eyequant-plugin-claude
claude plugin install eyequant@eyequant-marketplace
```

Ejemplos:

- «Muéstrame la señal de NVDA».
- «¿Cuántas señales abiertas hay en mi cuenta?».
- «Revisa el historial de SPY durante septiembre».
- «Agrega AAPL a mi watchlist principal».

Para validar la estructura con una instalación reciente de Claude Code:

```sh
claude plugin validate .
```

En el repositorio de la aplicación, valida `./plugins/eyequant` en lugar de `.`.

El plugin usa el transporte HTTP de MCP. Claude Code descubre las herramientas desde el servidor conectado; las firmas publicadas por él tienen prioridad sobre los ejemplos de la habilidad.
