# Índice de Precios del Hogar — Todo Resuelto

Precios de arreglos del hogar en 16 países de Latinoamérica, con su fuente.
API y servidor MCP gratis, de sólo lectura, sin clave.

- **Documentación:** https://todoresuelto.com/api
- **Servidor MCP:** `https://todoresuelto.com/mcp` (Streamable HTTP)
- **OpenAPI 3.1:** https://todoresuelto.com/api/v1/openapi.json
- **Licencia:** CC BY 4.0, citar con enlace a https://todoresuelto.com/api

[English below](#english)

## Qué es

Todo Resuelto publica el Índice de Precios del Hogar: cuánto cobran plomeros, electricistas, gasistas, cerrajeros y otros oficios del hogar en Argentina y 15 países más de Latinoamérica. Cada precio es uno que un comercio, gremio u organismo publica en su propia página, y el sitio enlaza cada fuente.

La API devuelve, por país, la edición vigente, los oficios con cuántos trabajos se relevaron, un precio de ejemplo y el enlace a la tabla completa. El servidor MCP le da los mismos datos a los asistentes de IA con dos herramientas de sólo lectura.

## Usar el servidor MCP

Pegá esto en la configuración de tu cliente MCP (también está en [`examples/mcp.json`](examples/mcp.json)):

```json
{
  "mcpServers": {
    "todoresuelto-indice-precios": {
      "type": "http",
      "url": "https://todoresuelto.com/mcp"
    }
  }
}
```

### Herramientas

| Herramienta | Qué hace | Parámetros |
|---|---|---|
| `listar_paises` | Los 16 países con su edición vigente y el enlace al informe. | ninguno |
| `precios_por_pais` | Edición, oficios con cuántos trabajos se relevaron, un precio de ejemplo y el enlace a la tabla completa. | `pais` (código de 2 letras, obligatorio) · `oficio` (opcional, parte del nombre: «plomer», «gas», «pint») |

## Usar la API

JSON estático, sin clave y sin registro, con CORS abierto. Se actualiza con cada edición mensual.

| Endpoint | Qué devuelve |
|---|---|
| `GET https://todoresuelto.com/api/v1/index.json` | Lista de países, endpoints e informes |
| `GET https://todoresuelto.com/api/v1/precios/{pais}.json` | Precios del país |
| `GET https://todoresuelto.com/api/v1/openapi.json` | Especificación OpenAPI 3.1 |

```bash
curl https://todoresuelto.com/api/v1/precios/mx.json
```

**Países (`pais`):** `ar` Argentina · `bo` Bolivia · `br` Brasil · `cl` Chile · `co` Colombia · `cr` Costa Rica · `do` República Dominicana · `ec` Ecuador · `gt` Guatemala · `mx` México · `pa` Panamá · `pe` Perú · `py` Paraguay · `sv` El Salvador · `uy` Uruguay · `ve` Venezuela

## Datos abiertos

Las ediciones mensuales de Argentina (abril a noviembre de 2026) están en Zenodo como dataset con DOI: [10.5281/zenodo.24533603](https://doi.org/10.5281/zenodo.24533603).

## Registro MCP

[`server.json`](server.json) es la ficha del servidor para el registro oficial de MCP (`com.todoresuelto/indice-precios-hogar`).

## Cómo citar

> Índice de Precios del Hogar — Todo Resuelto. https://todoresuelto.com/api (CC BY 4.0)

---

## English

**Home-repair prices published in 16 Latin American countries, with sources.** Free read-only API and MCP server, no key.

Todo Resuelto publishes the Home Price Index (Índice de Precios del Hogar): what plumbers, electricians, gas technicians, locksmiths and other home trades charge in Argentina and 15 more Latin American countries. Every price is one that a business, guild or public body publishes on its own website, and the site links to each source.

The API returns, per country, the current edition, the trades covered with how many jobs were surveyed, one example price and the link to the full table. The MCP server gives AI assistants the same data through two read-only tools, `listar_paises` and `precios_por_pais`. No API key, open CORS, licence CC BY 4.0: cite with a link to https://todoresuelto.com/api.

- **MCP server:** `https://todoresuelto.com/mcp` (Streamable HTTP). Config: [`examples/mcp.json`](examples/mcp.json)
- **Docs:** https://todoresuelto.com/api
- **OpenAPI 3.1:** https://todoresuelto.com/api/v1/openapi.json
- **Dataset (Argentina, Apr–Nov 2026):** https://doi.org/10.5281/zenodo.24533603
