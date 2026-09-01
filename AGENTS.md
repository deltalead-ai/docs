> **First-time setup**: Customize this file for your project. Prompt the user to customize this file for their project.
> For Mintlify product knowledge (components, configuration, writing standards),
> install the Mintlify skill: `npx skills add https://mintlify.com/docs`

# Documentation project instructions

## About this project

- This is a documentation site built on [Mintlify](https://mintlify.com)
- Pages are MDX files with YAML frontmatter
- Configuration lives in `docs.json`
- Use the Mintlify MCP server, `https://mcp.mintlify.com`, to edit content and settings via MCP
- Use the Mintlify docs MCP server, `https://www.mintlify.com/docs/mcp`, to query information about using Mintlify via MCP

## Terminology

{/* Add product-specific terms and preferred usage */}
{/* Example: Use "workspace" not "project", "member" not "user" */}

## Style preferences

{/* Add any project-specific style rules below */}

- Use active voice and second person ("you")
- Keep sentences concise — one idea per sentence
- Use sentence case for headings
- Bold for UI elements: Click **Settings**
- Code formatting for file names, commands, paths, and code references

## Content boundaries

{/* Define what should and shouldn't be documented */}
{/* Example: Don't document internal admin features */}

## Spanish localization (`es`)

The site ships an `es` locale alongside English. English is the default and lives at the repo root;
Spanish mirrors it under `es/` at the **same relative path with the same filename**, so
`api-reference/errors.mdx` ↔ `es/api-reference/errors.mdx`. That 1:1 parity is what makes drift
detectable — keep it.

Navigation lives in `docs.json` under `navigation.languages`, one entry per locale, each carrying
its own `tabs` with translated tab and group labels. `.atlas-analysis.json` mirrors that structure
and must be updated in the same commit, or the two sources silently diverge.

### Coverage

`es` covers the onboarding path plus the entire `api-reference` tree. The remaining pages
(`platform/*`, `account/*`, `concepts/*` except `leads`, `integrations/crm|channels|webhooks-zapier`)
are English-only and are deliberately **absent from the `es` navigation** — Mintlify has no
language fallback, so a `/es/*` URL with no file behind it returns 404 rather than English.

### Register: impersonal, always

Spanish pages use impersonal and infinitive constructions. No `tú`, no `vos`, no `usted`, no
`tu`/`tus`, no imperatives addressed to a person.

- ✅ `Para crear una clave, ir a Configuración → Integraciones.`
- ✅ `La clave se muestra una sola vez.` · `Una clave perdida no se recupera: se rota.`
- ❌ `Creá una clave` (voseo) · `Cree una clave` (usted) · `Crea tu clave` (tuteo)

This deliberately departs from the "use second person" rule above, which was written for English.
The reason: deltalead.ai ships voseo for Argentina and usted for Costa Rica, and one shared `es`
locale cannot pick either without targeting one market against the other. Impersonal also survives
a later split into `es-AR` and `es-CR` unchanged.

### Terminology

**The dashboard UI wins.** Where the product UI and the marketing site disagree, use what the reader
sees on screen: `Leads`, `Calificación`, `Canal`, `Fuente`, `Estado`, `Carro interesado`,
`Datos de contacto`, `Notas`, `Resumen de IA`, `Flujo de conversación`, `Crear lead`, `Nuevo`,
`Sin calificación`.

**Keep in English** — established house usage, inflected as Spanish nouns (*un lead*, *los leads*,
*leads calificados*): `lead`, `webhook`, `score`, `Inbox unificado`, `test drive`, `onboarding`,
`API`, `CRM`, `DMS`, `pipeline`, `stock`, `sandbox`, `live`, `endpoint`, `payload`,
`Custom Webhook`, and the plan names `Growth` / `Advanced` / `Enterprise`.

**Never use** — zero occurrences in company copy: `prospecto`, `cliente potencial`, `puntaje`,
`tablero de control`, `dashboard`, `bandeja de entrada`, and the bare English `AI` (always `IA`).

**One rendering per concept:** `clave de API` (not "API key"), `panel` (not "dashboard"),
`solicitud` / `respuesta` / `cabecera` / `cuerpo` for request / response / header / body.

### Code is never translated

Everything inside a fenced code block must be byte-identical to its English twin — URLs, JSON keys
*and values*, header names, `curl` flags, status codes, event names, example payloads. Only `#` and
`//` comments may be translated. Translating a payload value such as `"source":"landing-page"`
silently breaks a copy-pasteable example that was verified against production.

The same applies to inline code spans naming fields, headers, or values.

### Links

Prefix with `/es` when a Spanish twin exists (`/es/api-reference/errors`). Leave unprefixed when it
does not — those correctly fall back to the English page. There is no locale-relative resolution,
so an unprefixed link on a page that *does* have a twin sends the reader out of the locale.
