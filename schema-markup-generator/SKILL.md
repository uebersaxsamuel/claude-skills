---
name: schema-markup-generator
description: >
  Generate valid JSON-LD structured data for any page type. Supports Article,
  Product, FAQ, LocalBusiness, HowTo, Organization, BreadcrumbList, VideoObject,
  and more. Use when the user wants to add schema markup to improve rich results
  in Google Search. Trigger for phrases like "add schema markup", "create
  structured data", "JSON-LD for my page", "rich results", "schema.org",
  "FAQ schema", "product schema", or any request involving structured data
  for SEO purposes.
---

# Schema Markup Generator

A skill for generating error-free JSON-LD structured data that passes Google
Rich Results Test validation and maximises rich result eligibility.

---

## Phase 1 — Content Intake

Before generating any schema, **gather the following information** in a single
message. Do not skip this phase — missing data leads to invalid or incomplete markup.

**Always ask:**
1. **Page URL** — needed for `@id` and canonical references
2. **Page type** — What kind of page is this? (blog post, product, FAQ, about, service, tutorial, etc.)
3. **Available content** — Paste or describe the page content, OR share the URL so Claude can analyse it

**Detect automatically from content (ask only if unclear):**
- Business name, logo URL, contact details (for LocalBusiness / Organization)
- Author name, publish date, modified date (for Article)
- Product name, price, currency, availability (for Product)
- FAQ pairs: questions and answers (for FAQPage)
- Step-by-step instructions, tools, time estimates (for HowTo)
- Video title, description, thumbnail, duration, upload date (for VideoObject)
- Breadcrumb path and labels (for BreadcrumbList)

**Nice to have:**
- Site-wide brand name and logo
- Social media profile URLs
- Existing schema already on the page (to avoid duplicates)

---

## Phase 2 — Schema Type Detection

Map the page type to the correct schema(s):

| Page Type | Primary Schema | Common additions |
|---|---|---|
| Blog post / Article | `Article` or `BlogPosting` | `BreadcrumbList`, `Organization` (author) |
| News article | `NewsArticle` | `BreadcrumbList` |
| Product page | `Product` | `AggregateRating`, `Offer`, `Organization` |
| FAQ page / FAQ section | `FAQPage` | `BreadcrumbList` |
| Tutorial / Guide | `HowTo` | `BreadcrumbList` |
| Location / Contact page | `LocalBusiness` | `Organization`, `BreadcrumbList` |
| About page | `Organization` | `BreadcrumbList` |
| Video page | `VideoObject` | `BreadcrumbList` |
| Any page with breadcrumbs | `BreadcrumbList` | *(always add as supplement)* |
| Recipe | `Recipe` | `AggregateRating` |
| Event | `Event` | `Organization` |
| Course | `Course` | `Organization` |

**When multiple types apply → use `@graph` and output ALL schemas in one block.**

---

## Phase 3 — Generation Rules

Follow these rules strictly:

1. **Schema format depends on type** — see the Webflow Implementation Matrix below
2. **Use schema.org vocabulary exclusively** — never invent custom properties
3. **Nest schemas when appropriate** — e.g. `Organization` inside `Article.publisher`
4. **Use `@graph` for multiple JSON-LD schemas** — single `<script>` block, one `@context`
5. **Never invent data** — if a required field is missing, add a `// TODO:` comment inline AND note it in the checklist
6. **Use ISO 8601 dates** — e.g. `"2025-03-15"` or `"2025-03-15T09:00:00+01:00"`
7. **PriceValidUntil** — always include for Product schema; default to end of current year if not specified
8. **`@id` values** — use the canonical page URL + `#type` suffix (e.g. `https://example.com/page#article`)
9. **Image objects** — always use `ImageObject` with `url`, `width`, `height` when dimensions are known
10. **Telephone format** — always use E.164 format (e.g. `+41791234567`)

### Webflow Implementation Matrix

| Schema Type | Method | Placement |
|---|---|---|
| **FAQ** | HTML Microdata attributes on existing DOM | On the FAQ element itself in Webflow Designer |
| **BreadcrumbList** | HTML Microdata attributes on existing nav/list | On the breadcrumb nav element in Webflow Designer |
| **BlogPosting** (CMS) | JavaScript that reads DOM content + injects JSON-LD | Page Settings > Before `</body>` tag |
| **Organization** | JSON-LD `<script>` | Site Settings > Head Code |
| **LocalBusiness** / **Restaurant** | JSON-LD `<script>` | Site Settings > Head Code |
| **Person** | JSON-LD `<script>` | Page Settings > Head Code (About / Contact page) |
| **Product** | JSON-LD `<script>` | Page Settings > Head Code |
| **HowTo** | JSON-LD `<script>` | Page Settings > Head Code |
| **VideoObject** | JSON-LD `<script>` | Page Settings > Head Code |

**Key principle:** FAQ and BreadcrumbList are always implemented as HTML Microdata
in Webflow because the elements already exist in the DOM — no need to duplicate
content in a separate JSON-LD block.

---

## Phase 4 — Required & Recommended Properties per Type

### Article / BlogPosting
**Required:** `headline`, `author`, `datePublished`, `image`
**Recommended:** `dateModified`, `publisher` (Organization), `description`, `url`, `mainEntityOfPage`

### Product
**Required:** `name`
**Required for rich results:** `offers` (with `price`, `priceCurrency`, `availability`), `aggregateRating` OR `review`
**Recommended:** `description`, `image`, `brand`, `sku`, `offers.priceValidUntil`

### FAQPage
**Required:** `mainEntity` (array of `Question` with `name` + `acceptedAnswer.text`)
**Note:** Answers must be the complete answer — no "click here to read more"

### HowTo
**Required:** `name`, `step` (array of `HowToStep` with `text`)
**Recommended:** `totalTime`, `estimatedCost`, `tool`, `supply`, `image`, `description`
**Time format:** ISO 8601 duration — e.g. `"PT30M"` (30 min), `"PT1H"` (1 hour)

### LocalBusiness
**Required:** `name`, `address` (PostalAddress with `streetAddress`, `addressLocality`, `addressCountry`)
**Recommended:** `telephone`, `openingHoursSpecification`, `geo` (GeoCoordinates), `url`, `image`, `priceRange`

### Organization
**Required:** `name`, `url`
**Recommended:** `logo` (ImageObject), `contactPoint`, `sameAs` (array of social URLs), `address`

### BreadcrumbList
**Required:** `itemListElement` (array of `ListItem` with `position`, `name`, `item` URL)
**Note:** Home page is always position 1

### VideoObject
**Required:** `name`, `description`, `thumbnailUrl`, `uploadDate`
**Recommended:** `duration`, `contentUrl` or `embedUrl`, `publisher`

---

## Phase 5 — Output Format

Always output in this exact order:

### 1. JSON-LD Code Block
Complete, paste-ready `<script>` tag for the HTML `<head>`.

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    ...
  ]
}
</script>
```

### 2. Validation Checklist
A concise table showing required vs. recommended fields:

| Property | Status | Notes |
|---|---|---|
| `headline` | ✅ Present | — |
| `image` | ⚠️ Missing | Add hero image URL |
| `dateModified` | ✅ Present | — |

### 3. Rich Result Eligibility
State which rich result type(s) this schema enables:
- e.g. "**FAQ Rich Result** — eligible if page passes Google's content quality guidelines"
- e.g. "**Product Snippet** — eligible; AggregateRating will show star ratings"
- Include link to the relevant Google documentation page when possible

### 4. Implementation Notes
Any important notes for the developer:
- Where to place the script tag (always `<head>`)
- Whether to use a CMS plugin vs. manual paste
- Webflow-specific: use Embed element in `<head>` via Site Settings > Custom Code
- Validation tool: https://search.google.com/test/rich-results

---

## Phase 6 — Webflow-Specific Implementation

### FAQ Schema → HTML Microdata (preferred)

Add attributes directly to existing Webflow elements. No separate JSON-LD needed.

**Wrapper element** (e.g. the FAQ Section or Div):
```
itemscope=""
itemtype="https://schema.org/FAQPage"
```

**Each accordion/FAQ item** (the parent Div per question):
```
itemscope=""
itemprop="mainEntity"
itemtype="https://schema.org/Question"
```

**The question text element** (Heading or Paragraph):
```
itemprop="name"
```

**The answer wrapper Div**:
```
itemscope=""
itemprop="acceptedAnswer"
itemtype="https://schema.org/Answer"
```

**The answer text element** (Paragraph or RichText):
```
itemprop="text"
```

Full example of the resulting HTML structure:
```html
<div itemscope itemtype="https://schema.org/FAQPage">

  <div itemscope itemprop="mainEntity" itemtype="https://schema.org/Question">
    <h3 itemprop="name">Wie lange dauert ein Webflow-Projekt?</h3>
    <div itemscope itemprop="acceptedAnswer" itemtype="https://schema.org/Answer">
      <div itemprop="text">Je nach Umfang dauert ein typisches Projekt 4–8 Wochen.</div>
    </div>
  </div>

  <div itemscope itemprop="mainEntity" itemtype="https://schema.org/Question">
    <h3 itemprop="name">Was kostet eine Webflow-Website?</h3>
    <div itemscope itemprop="acceptedAnswer" itemtype="https://schema.org/Answer">
      <div itemprop="text">Preise starten ab CHF 3'000 für eine einfache Website.</div>
    </div>
  </div>

</div>
```

---

### BreadcrumbList Schema → HTML Microdata (preferred)

Add attributes to the existing breadcrumb nav element.

**Nav wrapper**:
```
itemscope=""
itemtype="https://schema.org/BreadcrumbList"
```

**Each breadcrumb item** (List item or Div):
```
itemscope=""
itemprop="itemListElement"
itemtype="https://schema.org/ListItem"
```

**The link inside each item**:
```
itemprop="item"
```

**The link text / span**:
```
itemprop="name"
```

**Hidden span for position** (add a hidden DOM element or use `content` attribute):
```html
<meta itemprop="position" content="1">
```

Full example:
```html
<nav itemscope itemtype="https://schema.org/BreadcrumbList">

  <div itemscope itemprop="itemListElement" itemtype="https://schema.org/ListItem">
    <a itemprop="item" href="https://example.com">
      <span itemprop="name">Home</span>
    </a>
    <meta itemprop="position" content="1">
  </div>

  <div itemscope itemprop="itemListElement" itemtype="https://schema.org/ListItem">
    <a itemprop="item" href="https://example.com/blog">
      <span itemprop="name">Blog</span>
    </a>
    <meta itemprop="position" content="2">
  </div>

  <div itemscope itemprop="itemListElement" itemtype="https://schema.org/ListItem">
    <a itemprop="item" href="https://example.com/blog/post-slug">
      <span itemprop="name">Post Title</span>
    </a>
    <meta itemprop="position" content="3">
  </div>

</nav>
```

---

### BlogPosting Schema → JavaScript (CMS-driven)

For Webflow CMS blog posts, use a `<script>` that reads content from the DOM
elements that Webflow already renders via CMS bindings. This avoids duplicating
content and keeps dates dynamic via Webflow's date transformers.

Place in **Page Settings > Before `</body>` tag** of the Blog Post template:

```html
<script>
/* BlogPosting Schema — reads from CMS-bound DOM elements */
document.addEventListener('DOMContentLoaded', function() {

  /* Read content from CMS-bound elements on the page */
  var summary = document.getElementById('post-summary')
    ? document.getElementById('post-summary').innerHTML : '';
  var content = document.getElementById('post-content')
    ? document.getElementById('post-content').innerHTML : '';

  var schemaData = {
    "@context": "https://schema.org",
    "@type": "BlogPosting",
    "headline": "{{Blog-Post-Titel}}",
    "image": "{{URL zum Hauptbild}}",
    "author": {
      "@type": "Person",
      "name": "{{Autor Name}}"
    },
    "publisher": {
      "@type": "Organization",
      "name": "{{Organisation Name}}",
      "logo": {
        "@type": "ImageObject",
        "url": "{{Logo URL}}"
      }
    },
    /* Webflow date transformer — outputs ISO 8601 format */
    "datePublished": "{{wf {\"path\":\"date\",\"transformers\":[{\"name\":\"date\",\"arguments\":[\"YYYY-MM-DDTHH:mm:ss+01:00\"]}],\"type\":\"Date\"} }}",
    "dateModified": "{{wf {\"path\":\"updated-on\",\"transformers\":[{\"name\":\"date\",\"arguments\":[\"YYYY-MM-DDTHH:mm:ss+01:00\"]}],\"type\":\"Date\"} }}",
    "mainEntityOfPage": {
      "@type": "WebPage",
      "@id": "https://www.example.com/blog/{{wf {\"path\":\"slug\",\"type\":\"PlainText\"} }}"
    },
    "description": summary,
    "articleBody": content
  };

  /* Inject schema into <head> */
  var script = document.createElement('script');
  script.type = 'application/ld+json';
  script.text = JSON.stringify(schemaData);
  document.head.appendChild(script);
});
</script>
```

**CMS setup for FAQ on Blog Posts:**
- Create a Multi-Reference field in the Blog Posts collection pointing to an FAQ collection
- The FAQ section uses HTML Microdata attributes (see FAQ section above) — no extra JS needed

---

### Other Schema Types → JSON-LD in `<head>`

| Schema | Location |
|---|---|
| Organization | Site Settings > Head Code |
| LocalBusiness / Restaurant | Site Settings > Head Code |
| Person | Page Settings > Head Code (About / Contact page) |
| Product | Page Settings > Head Code |
| HowTo | Page Settings > Head Code |
| VideoObject | Page Settings > Head Code |

---

## Quality Checks Before Output

Run through this checklist mentally before generating:

- [ ] No invented data — every value comes from provided content
- [ ] All required fields present (or `// TODO:` comments added)
- [ ] Dates in ISO 8601 format
- [ ] URLs are absolute (https://...), not relative
- [ ] `@id` values are unique across the `@graph`
- [ ] Telephone in E.164 format
- [ ] `PriceValidUntil` included for Product
- [ ] `acceptedAnswer.text` contains full answer text (no truncation)
- [ ] JSON is syntactically valid (no trailing commas, matched brackets)
- [ ] `@graph` used when multiple JSON-LD schema types are present
- [ ] FAQ → output as HTML Microdata attributes, not JSON-LD
- [ ] BreadcrumbList → output as HTML Microdata attributes, not JSON-LD
- [ ] BlogPosting (CMS) → output as JavaScript DOM-reader pattern, not static JSON-LD

---

## Example: Multi-Schema Output (Article + BreadcrumbList + Organization)

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [

    /* ── Article ──────────────────────────────────────── */
    {
      "@type": "BlogPosting",
      "@id": "https://example.com/blog/post-slug#article",
      "mainEntityOfPage": "https://example.com/blog/post-slug",
      "headline": "How to Build a Webflow Site in 2025",
      "description": "A complete beginner's guide to Webflow...",
      "datePublished": "2025-03-01",
      "dateModified": "2025-03-10",
      "image": {
        "@type": "ImageObject",
        "url": "https://example.com/images/hero.jpg",
        "width": 1200,
        "height": 630
      },
      "author": {
        "@type": "Person",
        "name": "Sam Uebersax",
        "url": "https://example.com/about"
      },
      "publisher": {
        "@id": "https://example.com#organization"
      }
    },

    /* ── Organization ─────────────────────────────────── */
    {
      "@type": "Organization",
      "@id": "https://example.com#organization",
      "name": "Uebersax Design GmbH",
      "url": "https://example.com",
      "logo": {
        "@type": "ImageObject",
        "url": "https://example.com/logo.png"
        /* TODO: Add width and height */
      },
      "sameAs": [
        "https://linkedin.com/company/example",
        "https://twitter.com/example"
      ]
    },

    /* ── BreadcrumbList ───────────────────────────────── */
    {
      "@type": "BreadcrumbList",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "name": "Home",
          "item": "https://example.com"
        },
        {
          "@type": "ListItem",
          "position": 2,
          "name": "Blog",
          "item": "https://example.com/blog"
        },
        {
          "@type": "ListItem",
          "position": 3,
          "name": "How to Build a Webflow Site in 2025",
          "item": "https://example.com/blog/post-slug"
        }
      ]
    }

  ]
}
</script>
```
