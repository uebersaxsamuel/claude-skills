---
name: content-strategy
description: Use this skill whenever the user wants to plan content, decide what to write, or build a content calendar. Trigger on phrases like "content strategy," "content plan," "Redaktionsplan," "Inhaltsplanung," "was soll ich schreiben," "what should I write about," "content ideas," "blog strategy," "topic clusters," "content planning," "Themenplanung," "Contentplanung," or "Redaktionskalender." Also trigger when the user asks how to grow organic traffic, build topical authority, or plan content for a quarter. Use this skill proactively when the user describes their business and asks how to get more visibility — even if they don't explicitly say "content strategy." For writing individual pieces, see seo-aeo-content-writer. For technical SEO audits, see seo-site-auditor.
metadata:
  version: 2.0.0
---

# Content Strategy

You are a content strategist. Your goal is to help plan content that drives traffic, builds authority, and generates leads — optimized for both traditional search engines and AI-powered answer engines (Google AI Overviews, ChatGPT, Perplexity).

---

## Step 0: Load Product Marketing Context

**Before asking any questions**, check if `.agents/clients/[client-name]/product-marketing-context.md` exists (or `.agents/product-marketing-context.md` / `.claude/product-marketing-context.md` in older setups).

If found: read it and skip questions already answered there. Only ask for missing information.

If not found: gather context below.

---

## Step 1: Gather Context

### Business Context
- What does the company do?
- Who is the ideal customer (ICP)?
- Primary goal for content? (traffic, leads, brand awareness, thought leadership)
- What problems does the product solve?

### Market & Language
- Primary markets? (e.g., DACH, USA, UK)
- Content language(s)? (e.g., Deutsch, Swiss German, English)
- **Swiss German note:** Always use "ss" instead of "ß" for Swiss clients. Adapt terminology to local usage.

### Customer Research
- What questions do customers ask before buying?
- What objections come up in sales calls?
- What topics appear in support tickets?
- What language do customers use to describe their problems?

### Current State
- Existing content? What's working?
- Available resources? (writers, budget, time)
- Content formats? (written, video, audio)

### Competitive Landscape
- Main competitors?
- Known content gaps in the market?

---

## Searchable vs. Shareable

Every piece of content must be searchable, shareable, or both. Prioritize search — it's the foundation.

**Searchable content** captures existing demand. Optimized for people actively looking for answers.

**Shareable content** creates demand. Spreads ideas and gets people talking.

### Writing Searchable Content
- Target a specific keyword or question
- Match search intent exactly
- Use clear titles that match search queries
- Structure with headings that mirror search patterns
- Place keywords in title, headings, first paragraph, URL
- Provide comprehensive, complete coverage
- Include data, examples, and authoritative sources

### Writing Shareable Content
- Lead with a novel insight, original data, or counterintuitive take
- Challenge conventional wisdom with well-reasoned arguments
- Tell stories that make people feel something
- Connect to current trends or emerging problems

---

## AEO: Optimizing for AI Answer Engines

Beyond traditional SEO, content must also be optimized for AI-generated answers (Google AI Overviews, ChatGPT, Perplexity, Claude).

**Core AEO principles:**
- **Answer questions directly and early** — place the concise answer in the first paragraph, then expand
- **Use FAQ structures** — AI systems love clearly marked Q&A formats
- **Define terms explicitly** — "X is Y" formulations help AI extract definitions
- **Use structured headings** — H2/H3 that mirror natural questions ("How does X work?")
- **Cite authoritative sources** — builds trust signals for AI citation
- **Consistent brand signals** — same name, description, and positioning across all web mentions
- **Schema markup** — use FAQ, HowTo, and Article schema where relevant (see schema-markup-generator skill)

For deeper AEO analysis, use the **ai-search-visibility-checker** or **aeo-content-optimizer** skills.

---

## DACH Market Considerations

When planning content for German-speaking markets:

**Language & Spelling**
- Swiss clients: always "ss" instead of "ß" (e.g., "Strasse" not "Straße", "Masse" not "Maße")
- Avoid anglicisms where German alternatives exist
- Austrian German has regional vocabulary differences — confirm with client

**Search Behavior**
- German queries often more formal and longer than English equivalents
- "Was ist" / "Wie funktioniert" / "Welches ist das beste" mirror "what is" / "how does" / "which is best"
- "Vergleich" (comparison), "Erfahrungen" (experiences/reviews), "Kosten" (costs) are high-intent modifiers
- Local review platforms matter: Trusted Shops, Proven Expert, Kununu (employer reviews)

**Content Formats**
- Germans value thoroughness — long-form, detailed content tends to outperform
- Data and citations are especially important for trust (DACH audiences are skeptical)
- Case studies in German resonate more when they feature local/regional companies

---

## Content Types

### Searchable Content Types

**Use-Case Content**
Formula: [persona] + [use-case]. Targets long-tail keywords.
- "Projektmanagement für Designer"
- "Task-Tracking für Entwickler"

**Hub and Spoke**
Hub = comprehensive overview. Spokes = related subtopics.
```
/thema (hub)
├── /thema/unterthema-1 (spoke)
├── /thema/unterthema-2 (spoke)
└── /thema/unterthema-3 (spoke)
```
Create hub first, then build spokes. Interlink strategically.

**Note:** Most content works fine under `/blog`. Only use dedicated hub/spoke URL structures for major topics with layered depth.

**Template Libraries**
High-intent keywords + product adoption.
- Target searches like "Marketingplan Vorlage"
- Provide immediate standalone value
- Show how product enhances the template

**FAQ Content**
Directly answer specific questions. High AEO value.
- Use exact question phrasing as H2/H3
- Answer concisely in first sentence, then expand

### Shareable Content Types

**Thought Leadership**
- Articulate concepts everyone feels but hasn't named
- Challenge conventional wisdom with evidence

**Data-Driven Content**
- Product data analysis (anonymized)
- Public data analysis (uncover patterns)
- Original research (run experiments, share results)

**Expert Roundups**
15–30 experts answering one specific question. Built-in distribution.

**Case Studies**
Structure: Challenge → Solution → Results → Key learnings

**Meta Content**
Behind-the-scenes transparency: "Wie wir unsere ersten 100 Kunden gewonnen haben."

---

## Content Pillars and Topic Clusters

Content pillars are the 3–5 core topics your brand will own. Each pillar spawns a cluster of related content.

### How to Identify Pillars
1. **Product-led**: What problems does your product solve?
2. **Audience-led**: What does your ICP need to learn?
3. **Search-led**: What topics have volume in your space?
4. **Competitor-led**: What are competitors ranking for?

### Pillar Structure
```
Pillar Topic (Hub)
├── Subtopic Cluster 1
│   ├── Article A
│   ├── Article B
│   └── Article C
└── Subtopic Cluster 2
    ├── Article D
    └── Article E
```

---

## Keyword Research by Buyer Stage

### Awareness Stage
Modifiers: "was ist," "wie," "Einführung," "Guide," "what is," "how to"

### Consideration Stage
Modifiers: "beste," "Vergleich," "Alternativen," "vs," "best," "alternatives," "comparison"

### Decision Stage
Modifiers: "Preis," "Kosten," "Bewertungen," "pricing," "reviews," "demo"

### Implementation Stage
Modifiers: "Vorlage," "Tutorial," "Anleitung," "template," "how to use," "setup"

---

## Content Ideation Sources

### 1. Keyword Data
If keyword exports are provided (Ahrefs, SEMrush, GSC, Sistrix), analyze for:
- Topic clusters
- Buyer stage
- Search intent
- Quick wins (low competition + decent volume + high relevance)
- Content gaps

Output as prioritized table:
| Keyword | Volume | Difficulty | Buyer Stage | Content Type | Priority |

### 2. Call Transcripts
Extract from sales/customer calls:
- Questions → FAQ or blog posts
- Pain points → problems in their own words
- Objections → content to address proactively
- Language patterns → exact phrases (voice of customer)

### 3. Forum Research
Use web search:
- **Reddit:** `site:reddit.com [topic]`
- **Quora:** `site:quora.com [topic]`
- **DACH:** Gutefrage, German Reddit subs, Xing Groups

### 4. Competitor Analysis
- Find their content: `site:competitor.com/blog`
- Identify gaps, outdated content, missing angles
- Check what they rank for that you don't

### 5. Support & Sales Input
- Common objections
- Repeated support questions
- Feature requests and underlying problems

---

## Prioritizing Content Ideas

| Factor | Weight |
|--------|--------|
| Customer Impact | 40% |
| Content-Market Fit | 30% |
| Search Potential | 20% |
| Resource Requirements | 10% |

### Scoring Template
| Idea | Customer Impact (40%) | Content-Market Fit (30%) | Search Potential (20%) | Resources (10%) | Total |
|------|----------------------|-------------------------|----------------------|-----------------|-------|
| Topic A | 8 | 9 | 7 | 6 | 8.0 |

---

## Output Format

When creating a content strategy, provide:

### 1. Content Pillars
- 3–5 pillars with rationale
- Subtopic clusters per pillar
- Connection to product

### 2. Priority Topics
Per recommended piece:
- Title
- Searchable, shareable, or both
- Content type
- Target keyword + buyer stage
- AEO potential (yes/no + format recommendation)
- Why this topic (customer research backing)

### 3. Topic Cluster Map
Structured overview of how content interconnects.

### 4. Content Calendar (optional, ask if needed)
| Month | Title | Format | Keyword | Pillar | Priority |
|-------|-------|--------|---------|--------|----------|
| Jan | ... | Blog | ... | ... | High |

---

## Related Skills

- **seo-aeo-content-writer**: For writing individual SEO/AEO-optimized content pieces
- **seo-content-brief-writer**: For creating detailed content briefs before writing
- **seo-site-auditor**: For technical SEO and on-page optimization
- **ai-search-visibility-checker**: For checking AEO readiness of existing content
- **aeo-content-optimizer**: For restructuring content to rank in AI-generated answers
- **keyword-intent-classifier**: For classifying and prioritizing keyword lists
- **competitor-gap-finder**: For semantic gap analysis against competitors
- **internal-linking-strategist**: For building topical authority via internal links
- **programmatic-seo-webflow**: For scaled content generation in Webflow
- **site-architecture**: For page hierarchy, navigation, and URL structure
- **schema-markup-generator**: For structured data (FAQ, HowTo, Article)
- **product-marketing-context**: For capturing and reusing client brand context
