---
name: seo-aeo-content-writer
description: >
  Creates fully SEO- and AEO-optimized articles, blog posts, landing page copy,
  and service pages. Use this skill whenever a user wants to write or improve
  web content that needs to rank in search engines, appear in AI-generated
  answers (ChatGPT, Perplexity, Google AI Overviews), or target a specific
  keyword. Trigger for phrases like "write a blog post", "create an article",
  "write SEO content", "optimize this text for search", "I need a landing page
  for [service]", "write content targeting [keyword]", or any request involving
  web copy that should be findable. Also trigger when the user wants to improve
  existing content for rankings or AI answer visibility.
---

# SEO & AEO Content Writer

A skill for producing publication-ready, search-optimized content that ranks
in both traditional SERPs and AI-generated answers (Google AI Overviews,
ChatGPT, Perplexity, Bing Copilot).

---

## Phase 1 — Brief Intake

Before writing anything, **always ask these three questions first** in a single
message — even if the user has already provided some context. Don't skip this.

**Mandatory upfront questions:**
1. **Tone of voice** — e.g. formal, friendly, technical, conversational, premium
2. **Target country / market** — Schweiz / Deutschland / Oesterreich / USA / UK / other
3. **Content type** — Blog post / Article / Guide / Service page / Landing page / FAQ page / Pillar page

Then also gather:

**Required**
- **Primary keyword** — the exact phrase to rank for
- **Target audience** — who is reading this? (persona, pain point, expertise level)
- **Desired length** — or let Claude recommend based on SERP analysis

**Nice to have**
- Secondary / LSI keywords
- Competitor URLs to beat
- CTA goal (generate leads, inform, convert)
- Internal links to include
- Existing content to improve (paste or upload)

If the user provides a URL, fetch it with `web_fetch` before writing.
If the user provides a keyword without context, do a quick `web_search`
to understand the current top-ranking content and SERP intent.

---

## Phase 2 — SERP & Intent Analysis

Before writing a single word, understand what Google currently rewards for
this keyword. This is the most important step — skipping it produces generic
content.

1. **Search** the primary keyword → identify the top 3–5 results
2. **Classify search intent**:
   - *Informational* → how-to, guide, explainer
   - *Commercial investigation* → comparison, review, best-of
   - *Transactional* → service page, landing page with CTA
   - *Navigational* → brand-specific (rare for content creation)
3. **Note**:
   - Average word count of top results
   - Heading structure (H2/H3 patterns)
   - Whether featured snippets exist (definition box, list, table)
   - Whether People Also Ask questions are present
   - Whether AI Overviews appear (signals AEO opportunity)

Use these observations to calibrate structure, depth, and format.

---

## Phase 3 — Content Architecture

Design the outline before writing. Present the outline to the user if they
want to approve before full draft (recommended for long-form content).

### Title & H1
- Include the primary keyword as early as possible
- Under 60 characters for SERP display
- Compelling enough to earn the click

### Meta Description
- 140–155 characters
- Include primary keyword naturally
- Add a value hook or call-to-action

### Content Structure Template
```
H1: [Primary keyword + value prop]
  Intro (100–150 words) — hook, problem, promise
  H2: [Topic cluster 1 — include secondary keyword]
    H3: Subtopic (if needed)
  H2: [Topic cluster 2]
  ...
  H2: FAQ (for AEO — structured Q&A)
  Conclusion + CTA
```

Adapt depth to intent:
- Informational blog: 1,200–2,500 words, rich subheadings, FAQs
- Service / landing page: 600–1,200 words, scannable, benefit-led, strong CTA
- Pillar page: 3,000+ words, covers all subtopics, links to cluster content

---

## Phase 4 — Writing Rules

### SEO Fundamentals
- **Primary keyword** in: H1, first 100 words, at least 2–3 H2s, meta description, URL slug suggestion
- **Keyword density**: 1–2% natural use — never stuff; write for humans first
- **LSI / semantic keywords**: weave in related terms Google associates with the topic
- **Internal links**: propose exactly 3 — see Internal Linking section below
- **External links**: propose exactly 2 credible outgoing references — see External Links section below
- **Image alt text suggestions**: include `[Image: descriptive alt text]` placeholders

### AEO (Answer Engine Optimization)

AEO makes content quotable by AI systems. Apply these patterns:

1. **Direct answer in the intro** — answer the primary query in 40–60 words in the first paragraph
   (Google uses this for featured snippets and AI Overviews)

2. **Definition sentences** — use the pattern `[Term] is [clear, standalone definition].`
   These get lifted verbatim by AI answer engines.

3. **Structured lists** — when explaining steps or options, use numbered or bulleted lists
   (AI systems parse these well)

4. **FAQ section** — always include 4–6 Q&A pairs at the end using the actual questions people ask
   (from PAA / search intent research). Format:
   ```
   **Q: [Question]**
   A: [40–80 word direct answer that stands alone without context]
   ```

5. **Schema markup suggestion** — at the end of the content, suggest the appropriate schema:
   - Blog/article → `Article` schema
   - FAQ section → `FAQPage` schema
   - Service page → `Service` + `LocalBusiness` schema
   - How-to → `HowTo` schema
   - Read `references/schema-templates.md` for ready-to-use JSON-LD snippets

### Internal Linking

Always propose exactly **3 internal link opportunities**. For each:
1. Identify a natural anchor text moment in the article
2. Suggest the most relevant existing page type the client likely has
3. Explain the SEO reason (passes link equity, deepens topical authority, reduces bounce)

Format in the deliverables:
```
## Internal Link Suggestions

1. Anchor: "[anchor text]"
   Place after: "[quote the sentence where it fits]"
   Suggested target: [page type / topic] — e.g. service page, related blog post
   Why: [1-sentence SEO rationale]

2. ...
3. ...
```

If the user has shared their sitemap or existing pages, use those.
If not, suggest the most logical page types based on the topic and content type.

### External Links & Outgoing References

Always propose exactly **2 outgoing links** to credible external sources.

**Before including any statistic or external source:**
1. Use `web_search` to find the original source (not a blog citing a blog)
2. Use `web_fetch` to verify the page is live, the stat is real, and the date is current
3. Apply this credibility filter:

| Source type | Credibility | Use? |
|-------------|-------------|------|
| Government / official bodies (admin.ch, bfs.ch, statista.com, gov.uk) | High | Yes |
| Academic / peer-reviewed (doi.org, university sites) | High | Yes |
| Industry research (Gartner, McKinsey, HubSpot, Semrush, Google) | High | Yes |
| Major journalism (NZZ, Handelsblatt, Reuters, BBC) | Medium-High | Yes, with date |
| Brand blogs / agency articles | Low | Avoid unless primary source |
| Forums, Reddit, Wikipedia | Low | Never as citation |

Format in the deliverables:
```
## Outgoing Link Suggestions

1. Anchor: "[anchor text]"
   URL: [verified URL]
   Source: [publication / organization]
   Stat / claim used: "[exact stat or claim]"
   Date verified: [YYYY-MM]
   Why credible: [1-sentence note]

2. ...
```

### Statistics & Data Rules

Content with real, sourced numbers builds E-E-A-T and gets cited by AI systems.
Follow this process for every statistic used:

1. **Search first** — don't use stats from memory; always verify with `web_search`
2. **Trace to primary source** — if a blog quotes a report, find the actual report
3. **Check date** — stats older than 3 years should be flagged or replaced
4. **Cite inline** — format: `[stat] (Source: [Organization], [Year])`
5. **Never invent** — if no credible source is found, don't include the stat

Example of correct inline citation:
> "Websites that load in under 2 seconds have a 15% higher conversion rate
> (Source: Google/Deloitte, 2023)."

### Readability
- Sentences under 20 words on average
- Paragraphs max 3–4 sentences
- Use subheadings every 200–300 words
- Use bold for key terms and scannable takeaways
- No jargon unless the target audience expects it

### Voice & Locale

Apply tone of voice from Phase 1 throughout. Then apply these locale rules:

| Market | Language rule | Tone default |
|--------|--------------|--------------|
| **Schweiz** | German — ALWAYS use "ss" instead of "ß" (e.g. "Strasse" not "Straße"). No exceptions. | Formal "Sie", neutral Hochdeutsch, measured — no hyperbole |
| **Deutschland** | Standard German with "ß" | Formal "Sie", can be slightly more direct/technical |
| **Oesterreich** | Standard German with "ß" | Formal "Sie", similar to DE |
| **USA** | American English | Friendly, benefit-led, active voice |
| **UK** | British English | Professional but warm, slight formality |

**Swiss rule is hard**: scan every word before output and replace any "ß" with "ss".

---

## Phase 5 — Deliverables Format

Always produce the full output as a structured document:

```
# [Article Title]

**Target keyword:** [primary keyword]
**Secondary keywords:** [comma-separated list]
**Search intent:** [informational / commercial / transactional]
**Recommended URL slug:** /[slug]
**Estimated read time:** X min

---

## Meta Title (≤60 chars)
[meta title here]

## Meta Description (140–155 chars)
[meta description here]

---

[FULL ARTICLE CONTENT]

---

## FAQ

**Q: [Question from PAA or search intent]**
A: [Direct 40–80 word answer]

[4–6 Q&A pairs total]

---

## Schema Markup

**Recommended type:** [Article / FAQPage / Service / HowTo / LocalBusiness]

[JSON-LD snippet — see references/schema-templates.md]

---

## Internal Link Suggestions

1. Anchor: "[anchor text]"
   Place after: "[sentence where it fits]"
   Suggested target: [page type / topic]
   Why: [SEO rationale]

2. Anchor: "[anchor text]"
   Place after: "[sentence where it fits]"
   Suggested target: [page type / topic]
   Why: [SEO rationale]

3. Anchor: "[anchor text]"
   Place after: "[sentence where it fits]"
   Suggested target: [page type / topic]
   Why: [SEO rationale]

## Outgoing Link Suggestions

1. Anchor: "[anchor text]"
   URL: [verified URL]
   Source: [organization]
   Stat / claim: "[stat used]"
   Date verified: [YYYY-MM]

2. Anchor: "[anchor text]"
   URL: [verified URL]
   Source: [organization]
   Stat / claim: "[stat used]"
   Date verified: [YYYY-MM]

## Optimization Checklist
- [ ] Primary keyword in H1
- [ ] Primary keyword in first 100 words
- [ ] Meta description under 155 chars
- [ ] FAQ section included
- [ ] Schema markup ready to implement
- [ ] 3 internal link placeholders added
- [ ] 2 outgoing links verified and sourced
- [ ] All statistics traced to primary source
- [ ] Image alt text suggestions included
```

---

## Phase 6 — Output Format Options

- **Markdown** (default) — for blog posts and articles; paste into Webflow CMS or any CMS
- **HTML** — if user is pasting into Webflow Rich Text block directly
- Offer Webflow users: "I can format this as clean HTML with correct heading tags
  for Webflow's Rich Text editor — want that instead?"

---

## Quick Reference: Optimization Priority

| Goal | What matters most |
|------|-------------------|
| Rank in Google SERP | Keyword placement, E-E-A-T signals, content depth |
| Appear in AI Overviews | Direct answers, definitions, structured lists |
| Get cited by ChatGPT/Perplexity | Authoritative statements, factual density, schema |
| Convert visitors | Clear CTA, benefit-led copy, social proof |

Build content that satisfies all four — they rarely conflict.

---

## References

Read these when you need deeper guidance:
- `references/schema-templates.md` — ready-to-use JSON-LD for all schema types
- `references/keyword-research.md` — keyword clustering, intent mapping, SERP feature targeting
- `references/german-seo.md` — German-language SEO specifics, DACH market nuances
