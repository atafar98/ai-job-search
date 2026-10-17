# Search Queries for Job Scraper

## Candidate: Rafael González Seliva
## Location base: Terrassa, Barcelona, España
## Salary minimum: 48.000 € brutos anuales
## Remote: Fully remote (any location), or hybrid in Barcelona area only, or on-site in Terrassa/Sabadell only

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`. The Danish portal demos ship disabled — not relevant for the Spanish market.

The `site:` query templates below are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** Rafael works in Spanish and English (B2). Queries are written in both languages. Catalan postings are also acceptable (native), but most Catalan-market postings appear in Spanish or English.

## Search Sites

Primary (Spanish market):
- **infojobs.net** — Spain's largest general job board
- **tecnoempleo.com** — Spain's main tech-specific job board
- **linkedin.com/jobs** — LinkedIn (also covered by `linkedin-search` CLI)
- **jobteaser.com** — used by some tech companies in Spain

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for known target companies

## Query Categories

### Priority 1: Senior Frontend / Angular Developer

Core role — strongest match, most desired direction.

```
site:infojobs.net "Senior Frontend Developer" Angular Barcelona
site:infojobs.net "Desarrollador Frontend Senior" Angular Barcelona
site:tecnoempleo.com "Senior Frontend Developer" Angular Barcelona
site:tecnoempleo.com "Desarrollador Frontend Senior" Angular Barcelona
site:infojobs.net "Angular Developer" Senior Barcelona
site:tecnoempleo.com "Desarrollador Angular" Senior Barcelona
site:linkedin.com/jobs "Senior Frontend Developer" Angular Barcelona
site:linkedin.com/jobs "Senior Angular Developer" España
site:infojobs.net "Frontend Developer" Angular remoto España
site:tecnoempleo.com "Frontend Developer" Angular remoto
```

### Priority 2: Frontend Architecture / Tech Lead

Roles with architectural mandate or team leadership component.

```
site:infojobs.net "Frontend Architect" Barcelona
site:tecnoempleo.com "Arquitecto Frontend" Barcelona
site:infojobs.net "Frontend Tech Lead" Angular Barcelona
site:tecnoempleo.com "Tech Lead Frontend" Angular Barcelona
site:infojobs.net "Lead Frontend Developer" Barcelona
site:linkedin.com/jobs "Frontend Tech Lead" Angular España
site:linkedin.com/jobs "Frontend Architect" Angular España
site:infojobs.net "referente técnico frontend" Angular Barcelona
```

### Priority 3: Adjacent Roles (broader pivot)

Roles Rafael could step into given his profile.

```
site:infojobs.net "Developer Experience" Engineer Barcelona
site:tecnoempleo.com "DX Engineer" Frontend Barcelona
site:infojobs.net "Full Stack Developer" Angular TypeScript Barcelona
site:tecnoempleo.com "Desarrollador Full Stack" Angular TypeScript Barcelona
site:infojobs.net "Frontend Engineer" Angular TypeScript Barcelona
site:linkedin.com/jobs "Frontend Engineer" Angular TypeScript España
site:infojobs.net "Consultor técnico" Frontend Angular Barcelona
```

### Priority 4: Remote-only broad search (wider net)

For fully remote roles anywhere in Spain or internationally.

```
site:infojobs.net "Angular Developer" remoto España
site:tecnoempleo.com "Frontend Developer" Angular remoto España
site:linkedin.com/jobs "Angular Developer" remote Spain
site:linkedin.com/jobs "Senior Frontend Developer" remote España
site:infojobs.net Angular TypeScript remoto "Senior"
site:tecnoempleo.com Angular TypeScript teletrabajo Senior
```

### Target company career pages (direct)

```
site:circontrol.com/careers
site:capgemini.com/es-es/careers
site:thoughtworks.com/es-es/careers Angular
site:adevinta.com/careers Angular
site:king.com/careers Frontend Angular
site:softonic.com/careers Frontend
site:typeform.com/careers Frontend Angular
```

## Location Filter

When evaluating results, verify the job location:

| Location | Verdict |
|---|---|
| 100% remote (anywhere) | **PASS** |
| Hybrid — Barcelona ciudad o área metropolitana (Terrassa, Sabadell, Hospitalet, Badalona, etc.) | **PASS** |
| Hybrid — up to ~40 min from Terrassa by transit | **PASS** |
| On-site — Terrassa o Sabadell | **PASS** |
| On-site — Barcelona ciudad (daily commute) | **FLAG** — discuss with user |
| Hybrid or on-site — Madrid, Valencia, or other city requiring relocation | **FAIL** — deal-breaker |
| Relocation required | **FAIL** — deal-breaker |

## Salary Filter

Minimum: **48.000 € brutos anuales**. If salary is not listed in the posting, do not reject — flag as "salary unknown" and proceed to evaluation. If salary range is explicitly below 48k, flag as below minimum.

## Language Filter

Working languages: Spanish (native), Catalan (native), English (B2).

Apply `04-job-evaluation.md`'s Language Gate:
- A posting requiring a language not declared (e.g. French, German) → **FAIL**
- A posting requiring "fluent English" or "C1/C2 English" → **FLAG** (B2 declared — let Rafael decide)
- A posting in English for a role that only needs Spanish/Catalan on the job → **PASS**

## Date Filter

Only include jobs posted within the last 14 days, or with an application deadline that has not yet passed. If a posting date cannot be determined, include it but flag as "date unknown".

## Adapting Queries

If the user specifies a focus area, select queries from the matching category and also generate 2-3 custom queries for that focus. For example:
- `/scrape remote` → Priority 4 queries + remote-specific variants
- `/scrape tech lead` → Priority 2 queries + leadership-specific variants
- `/scrape Angular` → Priority 1 + all Angular variants across categories
