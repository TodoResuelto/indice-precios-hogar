# Índice de Precios del Hogar — Todo Resuelto

Precios de arreglos del hogar en 16 países de Latinoamérica, con su fuente.
API y servidor MCP gratis, de sólo lectura, sin clave.

- **Sitio:** [Todo Resuelto](https://todoresuelto.com)
- **Precios:** [Índice de Precios del Hogar](https://todoresuelto.com/informe-precios-hogar)
- **Servidor MCP:** `https://todoresuelto.com/mcp` (Streamable HTTP)
- **OpenAPI 3.1:** `https://todoresuelto.com/api/v1/openapi.json`
- **Licencia:** CC BY 4.0, citar con enlace a [todoresuelto.com](https://todoresuelto.com)

[English below](#english)

## Qué es

Todo Resuelto publica el Índice de Precios del Hogar: cuánto cobran plomeros, electricistas, gasistas, cerrajeros y otros oficios del hogar en Argentina y 15 países más de Latinoamérica. Cada precio es uno que un comercio, gremio u organismo publica en su propia página, y el sitio enlaza cada fuente.

La API devuelve, por país y por oficio, **una muestra de hasta 3 trabajos con su rango, su unidad y su fuente** (quién publica ese precio y el enlace a la página donde lo publica), cuántos trabajos tiene la tabla completa y el enlace a esa tabla, donde están todas las filas y todas las fuentes. El servidor MCP le da los mismos datos a los asistentes de IA con dos herramientas de sólo lectura.

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
| `precios_por_pais` | Por oficio: hasta 3 trabajos con rango y fuente, cuántos trabajos tiene la tabla completa y el enlace a esa tabla. | `pais` (código de 2 letras, obligatorio) · `oficio` (opcional, parte del nombre: «plomer», «gas», «pint») |

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

Respuesta (recortada):

```json
{
  "pais": "México",
  "moneda": "MXN",
  "edicion": "2026-11-01",
  "muestra_explicacion": "Por oficio, una muestra de hasta 3 trabajos con su rango y su fuente. La tabla completa, con todas las filas y todas las fuentes, está en `tabla_completa`.",
  "oficios": [
    {
      "oficio": "Plomería",
      "trabajos_relevados": 57,
      "muestra": [
        {
          "trabajo": "Destape básico",
          "min": 1800,
          "max": 2300,
          "moneda": "MXN",
          "unidad": "por trabajo",
          "zona": "Monterrey y área metropolitana",
          "fuente": { "nombre": "Plomero Apodaca", "tipo": "empresa", "url": "https://plomeroapodaca.com/cuanto-cobra-un-plomero-por-destapar-un-drenaje/", "fecha": "2026-11-01" }
        }
      ],
      "tabla_completa": "https://todoresuelto.com/mx/precios/plomeria"
    }
  ]
}
```

Con Claude Code:

```bash
claude mcp add --transport http todoresuelto https://todoresuelto.com/mcp
```

**Países (`pais`):** `ar` Argentina · `bo` Bolivia · `br` Brasil · `cl` Chile · `co` Colombia · `cr` Costa Rica · `do` República Dominicana · `ec` Ecuador · `gt` Guatemala · `mx` México · `pa` Panamá · `pe` Perú · `py` Paraguay · `sv` El Salvador · `uy` Uruguay · `ve` Venezuela

## Datos abiertos

Las ediciones mensuales de Argentina (abril a noviembre de 2026) están en Zenodo como dataset con DOI: [10.5281/zenodo.24533603](https://doi.org/10.5281/zenodo.24533603).

## Registro MCP

[`server.json`](server.json) es la ficha del servidor para el registro oficial de MCP (`com.todoresuelto/indice-precios-hogar`).

## Cómo citar

> [Índice de Precios del Hogar — Todo Resuelto](https://todoresuelto.com/informe-precios-hogar) (CC BY 4.0)

---

## English

**Home-repair prices published in 16 Latin American countries, with sources.** Free read-only API and MCP server, no key.

Todo Resuelto publishes the Home Price Index (Índice de Precios del Hogar): what plumbers, electricians, gas technicians, locksmiths and other home trades charge in Argentina and 15 more Latin American countries. Every price is one that a business, guild or public body publishes on its own website, and the site links to each source.

The API returns, for each country and trade, **up to 3 sample jobs with their price range, unit and source** (who publishes that price and the URL of the page), how many jobs the full table prices, and the link to that full table with every row and source. The MCP server gives AI assistants the same data through two read-only tools, `listar_paises` and `precios_por_pais`. No API key, open CORS, licence CC BY 4.0: cite with a link to [todoresuelto.com](https://todoresuelto.com).

- **MCP server:** `https://todoresuelto.com/mcp` (Streamable HTTP). Config: [`examples/mcp.json`](examples/mcp.json)
- **Site:** [Todo Resuelto](https://todoresuelto.com) · **Prices:** [Home Price Index](https://todoresuelto.com/informe-precios-hogar)
- **OpenAPI 3.1:** `https://todoresuelto.com/api/v1/openapi.json`
- **Dataset (Argentina, Apr–Nov 2026):** https://doi.org/10.5281/zenodo.24533603

## Changelog

- **1.1.0:** each trade now carries up to 3 sample jobs with range, unit and source; OpenAPI with response schemas. / Cada oficio trae hasta 3 trabajos con rango, unidad y fuente.
- **1.0.0 (25-nov-2026):** first release: API, MCP server, official MCP Registry.

## Contacto

hola@todoresuelto.com

