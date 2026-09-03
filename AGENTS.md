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

**Spanish is the default locale and lives at the repo root.** English mirrors it under `en/` at the
**same relative path with the same filename**, so `api-reference/errors.mdx` (Spanish) ↔
`en/api-reference/errors.mdx` (English). That 1:1 parity is what makes drift detectable — keep it.
Adding a page means adding both halves in the same commit.

Navigation lives in `docs.json` under `navigation.languages`, one entry per locale, each carrying
its own `tabs` with translated tab and group labels. `.atlas-analysis.json` mirrors that structure
and must be updated in the same commit, or the two sources silently diverge.

### Coverage

Both locales cover all 29 navigated pages. Mintlify has no language fallback — a URL with no file behind it
returns 404, never the other language — so parity is not optional once a page is in either
navigation.

Pages for endpoints that are drafted but not yet served are parked as `*.draft.mdx`, which
`.mintignore` excludes from the build. Both locale halves are renamed together, so parity holds for
drafts too. Publishing one means renaming both halves back and adding both nav entries — never
before the route answers on `platform-api-dev`.

The Spanish navigation is generated from the English structure rather than maintained by hand; only
tab and group labels are translated. Keep it that way, so the two trees cannot drift in shape.

URLs from the previous layout, when English sat at the root and Spanish under `es/`, are covered by
a wildcard redirect `/es/:slug*` → `/:slug*` in `docs.json`. Do not remove it.

### Register: impersonal, always

Spanish pages use impersonal and infinitive constructions. No `tú`, no `vos`, no `usted`, no
`tu`/`tus`, no imperatives addressed to a person.

- ✅ `Para crear una clave, ir a Organización → Integraciones.`
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

There is no locale-relative link resolution, so every internal link carries its locale explicitly.
Spanish pages link bare (`/api-reference/errors`); English pages under `en/` link with the prefix
(`/en/api-reference/errors`). An unprefixed link inside an English page silently sends the reader
into the Spanish site.
