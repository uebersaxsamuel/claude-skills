---
name: programmatic-seo-webflow
description: >
  Use when the user wants to implement programmatic SEO specifically in Webflow.
  Triggers: "pSEO in Webflow", "Webflow CMS for SEO pages at scale", "dynamic pages Webflow",
  "collection template SEO", "bulk import Webflow CMS", "location pages Webflow",
  "nested collections Webflow", "HTMX Webflow CMS", "vdx Webflow".
  For general pSEO strategy see programmatic-seo. For auditing see seo-audit.
metadata:
  version: 1.0.0
---

# Programmatic SEO – Webflow Implementation

You are an expert in building programmatic SEO pages at scale using Webflow CMS.
Your goal: scalable, rankable, technically sound pages—built natively in Webflow.

---

## Initial Assessment

Before starting, clarify:

1. **Playbook Type** – Which pSEO pattern? (Locations, Personas, Comparisons, Glossary, etc.)
2. **Data Source** – CSV/Airtable/Make.com/manual? How many items?
3. **Nesting Required?** – Do pages need data from multiple collections? (→ use HTMX or vdx)
4. **Scale** – How many CMS items? Webflow limit: **10,000 items per collection**.
5. **Languages** – Single language or multi-locale (Webflow Localization)?

---

## Core Webflow Concepts for pSEO

### CMS Collections as Page Factories

Each Webflow CMS Collection with a **Collection Template Page** generates one URL per item:

```
Collection: /locations → Template: /locations/[slug]
Collection: /integrations → Template: /integrations/[slug]
```

One collection = one URL pattern. For multiple patterns, use multiple collections.

### Slug = URL

The `slug` field controls the URL. Always:
- Use lowercase, hyphens only
- Keep it short and keyword-rich
- Set it explicitly on import (don't rely on auto-generation from Name)

**Good**: `webflow-designer-zurich`
**Bad**: `webflow-designer-zrich-1`

---

## CMS Collection Design by Playbook

### Locations – `/[service]/[city]/`

| Field | Type | Purpose |
|-------|------|---------|
| Name | Plain Text | "Webflow Designer in Zürich" |
| Slug | Plain Text | `webflow-designer-zurich` |
| City | Plain Text | Zürich |
| Region | Plain Text | Zürich |
| Country | Reference → Countries | Switzerland |
| Intro Copy | Rich Text | Unique intro per location |
| Local Stats | Plain Text | e.g. "120+ Webflow projects" |
| Meta Title | Plain Text | SEO title |
| Meta Description | Plain Text | SEO description |
| OG Image | Image | Per-page open graph |
| Noindex | Switch | Deactivate thin pages |

### Comparisons – `/compare/[x]-vs-[y]/`

| Field | Type | Purpose |
|-------|------|---------|
| Product A | Reference → Products | |
| Product B | Reference → Products | |
| Slug | Plain Text | `webflow-vs-wordpress` |
| Summary | Rich Text | Unique comparison summary |
| Winner Use Case A | Plain Text | "Best for designers" |
| Winner Use Case B | Plain Text | "Best for blogs" |
| Feature Table | Rich Text or Embed | Side-by-side comparison |
| Schema Type | Plain Text | `Product` or `FAQPage` |

### Glossary – `/glossary/[term]/`

| Field | Type | Purpose |
|-------|------|---------|
| Term | Plain Text | "Cumulative Layout Shift" |
| Slug | Plain Text | `cumulative-layout-shift` |
| Short Definition | Plain Text | Used in meta description |
| Full Definition | Rich Text | Page body |
| Related Terms | Multi-Reference → Glossary | Internal linking |
| Category | Option | e.g. "Core Web Vitals" |

### Personas – `/for/[audience]/`

| Field | Type | Purpose |
|-------|------|---------|
| Persona | Plain Text | "SaaS Startups" |
| Slug | Plain Text | `saas-startups` |
| Pain Points | Rich Text | Audience-specific |
| Features Highlighted | Multi-Reference → Features | |
| Testimonial | Reference → Testimonials | Persona-matched |
| CTA Label | Plain Text | Custom CTA per persona |

---

## Bulk Import via CSV

### Workflow

1. **Prepare CSV** – Match column headers exactly to Webflow field names
2. **Generate slugs** in CSV (formula: `=LOWER(SUBSTITUTE(A2," ","-"))`)
3. **Import** via Webflow Designer → CMS → Collection → Import
4. **Review** – Check 10–20 items for slug accuracy and field mapping
5. **Publish** selectively – Only publish items with sufficient unique content

### CSV Tips

- Reference fields: Use the referenced item's **Name** (not ID) for import
- Multi-Reference: Not importable via CSV → use Make.com or Webflow API
- Switch fields: Use `true` / `false` in CSV
- Rich Text: Plain text only on import; format after import or use HTML via API

### At Scale: Webflow API + Make.com

For 500+ items or complex data:
```
Data Source (Airtable/Google Sheets)
  → Make.com Scenario
    → Webflow API: Create CMS Item
      → Publish via API after QA
```

---

## Nested Collections (Without Finsweet)

Webflow's native CMS lists cannot load items from a *different* collection dynamically on a Collection Template page. Two solutions:

### Option A: HTMX

Load related items from another collection via a Webflow-hosted endpoint or proxy.

```html
<!-- Load related blog posts for current category -->
<div
  hx-get="/cms-proxy?collection=posts&category={{wf-field:slug}}"
  hx-trigger="load"
  hx-swap="innerHTML">
  <p>Loading related posts…</p>
</div>
```

**Setup**:
1. Deploy a lightweight proxy (Cloudflare Worker or Vercel Edge Function)
2. Proxy calls Webflow CMS API filtered by slug/reference
3. Returns HTML fragment
4. HTMX injects it into the page

**Best for**: Related items, "You might also like", cross-collection lookups.

### Option B: VisualDX Library

[VisualDX](https://www.visualdx.dev/) ist eine kostenlose, attribute-basierte JavaScript Library speziell für Webflow. Keine Backend-Proxy nötig — alles läuft über `vdx-*` Custom Attributes direkt im Webflow Designer.

**Setup** (einmalig):
```html
<!-- Vor </body> im globalen Footer Code einfügen -->
<script src="https://cdn.visualdx.dev/v1/vdx.js"></script>
```

**Nested Collections mit vdx** — 3 Schritte:

**Schritt 1**: Im Parent Collection List Item → Text Link auf "Current Item" Collection Page setzen, Custom Attribute hinzufügen:
```
Name:  vdx-nest-link
Value: card
```

**Schritt 2**: Auf der Child Collection Template Page → Collection List hinzufügen (gefiltert nach aktuellem Item), Custom Attribute:
```
Name:  vdx-nest-list
Value: card
```

**Schritt 3**: Publizieren — VisualDX fetcht die Child-Liste clientseitig und injiziert sie in die Parent-Items.

**Best for**: Related items, Hub-and-spoke links, Tags/Kategorien auf Collection Templates.

**Comparison**:

| | HTMX | VisualDX |
|--|------|----------|
| Backend needed | Yes (proxy) | No |
| Setup complexity | Medium | Low |
| Flexibilität | Sehr hoch | Medium |
| Performance | Abhängig vom Proxy | Schnell (client-side) |
| Best for | Custom logic, API calls | Nested CMS Lists |

---

## SEO Fields per CMS Item

Every collection used for pSEO pages needs these fields:

| Field | Type | Notes |
|-------|------|-------|
| Meta Title | Plain Text | 50–60 chars, bind in Page Settings |
| Meta Description | Plain Text | 140–160 chars |
| OG Image | Image | 1200×630px |
| Canonical URL | Plain Text | Nur wenn Duplicate-Control nötig |

**Binding in Webflow**:
Collection Template → Page Settings → SEO Tab → Connect to CMS fields.

### Indexation per Collection steuern

Webflow bietet keinen Noindex-Switch mehr auf Item-Ebene. Stattdessen:

- **Ganze Collection deindexieren**: Collection Settings → Publishing Toggle deaktivieren → alle Template Pages verschwinden aus Sitemap und werden nicht gecrawlt
- **Einzelne Items**: Nicht nativ möglich. Workaround: Eigene Collection für "thin" Items anlegen und deren Publishing deaktivieren
- **Thin-Content-Strategie**: Lieber weniger Items publizieren und mit Qualität skalieren, als später manuell deindexieren müssen

---

## Schema Markup via Custom Code Embed

Use a Code Embed element inside the Collection Template to inject JSON-LD dynamically.

### Example: LocalBusiness Schema

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "{{wf-field:name}}",
  "description": "{{wf-field:short-description}}",
  "address": {
    "@type": "PostalAddress",
    "addressLocality": "{{wf-field:city}}",
    "addressCountry": "{{wf-field:country}}"
  },
  "url": "https://yoursite.com/locations/{{wf-field:slug}}"
}
</script>
```

**Important**: Webflow's `{{wf-field:}}` syntax only works inside **Embed** elements on Collection Templates—not in custom code in `<head>`.

For `<head>` injection, use a workaround:
1. Add a hidden `<div id="schema-data">` with CMS fields as data attributes
2. Read attributes via JS and inject JSON-LD into `<head>`

---

## Internal Linking Architecture

### Hub-and-Spoke in Webflow

**Hub page** (static or CMS): `/locations/`
**Spoke pages** (CMS Template): `/locations/[city]/`

On the Hub page:
- Add a Collection List bound to the Locations collection
- Filter/sort as needed
- Link each item to its template page

On each Spoke page (Template):
- Collection List: "Other locations in [Country]" → filter by same Country Reference
- Collection List: "Related services" → Multi-Reference field

### Avoiding Orphan Pages

- Every CMS item must be linked from at least one Collection List somewhere on the site
- Add new collections to the main sitemap hub page
- Use Webflow's built-in XML sitemap (auto-includes all published CMS items)

---

## Webflow-Specific Limits & Constraints

| Limit | Value | Workaround |
|-------|-------|-----------|
| Items per collection | 10,000 | Split into multiple collections |
| Collections per site | 40 | Plan architecture carefully |
| Reference fields per item | 1 (Reference) | Use Multi-Reference or restructure |
| Multi-Reference items | 25 per field | Flatten data if needed |
| Collection list per page | 20 | Pagination or HTMX/vdx for more |
| Nesting depth (native) | 1 level | Use HTMX or vdx for deeper nesting |
| CSV import (Rich Text) | Plain text only | Use Webflow API for formatted content |

---

## Quality Checklist (Webflow-Specific)

**Before publishing:**
- [ ] Slug matches intended URL pattern
- [ ] Meta Title and Meta Description fields filled (not empty)
- [ ] OG Image assigned
- [ ] Collection Publishing aktiviert (sonst erscheinen keine Template Pages in Sitemap)
- [ ] Schema Embed present and CMS fields bound
- [ ] At least one Collection List links to this item from elsewhere
- [ ] Unique content field (intro, local stats, etc.) is filled—not a template default

**After publishing:**
- [ ] Test URL in browser
- [ ] Validate schema via [schema.org validator](https://validator.schema.org)
- [ ] Submit sitemap to Google Search Console
- [ ] Check "URL Inspection" for a sample of items

---

## Common Mistakes (Webflow-Specific)

- **Identical Rich Text across all items**: Webflow has no native conditional content—use Switch fields + conditional visibility blocks
- **Empty SEO fields**: Webflow falls back to page name/description, which is often wrong for pSEO
- **Auto-slugs from Name**: Webflow slugifies the Name field, but special characters (ü, ö, ä) can create ugly URLs—set slugs explicitly
- **Alle Items auf einmal publizieren**: QA erst an einer Auswahl durchführen; thin Items besser in separater Collection mit deaktiviertem Publishing halten
- **Forgetting to bind SEO fields**: CMS fields exist but aren't connected to Page Settings SEO section

---

## Related Skills

- **programmatic-seo**: General pSEO strategy and playbook selection
- **seo-audit**: Auditing pSEO pages post-launch
- **schema-markup**: Detailed schema implementation
- **webflow-cms**: General Webflow CMS management
