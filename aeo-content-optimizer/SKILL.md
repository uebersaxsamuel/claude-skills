---
name: aeo-content-optimizer
version: 1.0.1
description: >
  Restructures existing content to rank in AI-generated answers from ChatGPT,
  Perplexity, Claude, and Google AI Overviews. Use this skill whenever a user
  wants to optimize, rewrite, or audit existing content for Answer Engine
  Optimization (AEO). Trigger for phrases like "optimize this for AI answers",
  "make this rankable in AI search", "improve AEO", "restructure for Perplexity",
  "get cited by ChatGPT", "optimize for Google AI Overviews", or any request
  to improve how AI systems quote or reference existing content. Also trigger
  when the user pastes content and asks how to make it more likely to appear
  as an AI-cited source.
---

# AEO Content Optimizer

A skill for restructuring existing content so AI search systems (Google AI
Overviews, ChatGPT, Perplexity, Claude) cite it as a source when answering
user queries.

---

## Phase 1 — Input Collection

Before optimizing anything, confirm these three things in a single message:

1. **Target query** — What exact search phrase should this content rank for?
2. **Primary AI platform** — Google AI Overviews / Perplexity / ChatGPT / all?
3. **Content language / market** — Schweiz (ss statt ß) / Deutschland / Oesterreich / other?

Then ask the user to paste the existing content if not already provided.

---

## Phase 2 — Platform Intelligence

Each AI answer engine has different selection preferences:

| Platform | What it favours |
|---|---|
| **Google AI Overviews** | See Google-specific section below |
| **Perplexity** | Factual accuracy, numbered lists, cited data points, clear source attribution |
| **ChatGPT** | Comprehensive context, conversational flow, definitions alongside facts |
| **Claude** | Nuanced multi-perspective analysis, precise language, structured reasoning |

Default to optimizing for all four unless the user specifies otherwise.

---

### 🔵 Google AI Overviews — Official Guidance (Google-specific only)

Source: [Google Search Central AI Optimization Guide](https://developers.google.com/search/docs/fundamentals/ai-optimization-guide) (updated June 2026)

**How Google AI selects content:**
- **RAG (Retrieval-Augmented Generation):** Google's AI Overviews are grounded in the core Search index. A page must be **indexed and snippet-eligible** to appear — this is a hard technical requirement.
- **Query fan-out:** Google generates concurrent sub-queries from the original search. Content with sufficient depth and topical coverage is more likely to be retrieved across multiple fan-out queries.

**What matters for Google AI (Google-specific):**
- Unique, non-commodity content with a clear point of view — first-hand experience, expert takes, original analysis
- Helpful, people-first content (E-E-A-T signals remain relevant)
- Clear page structure with headings for human readability
- High-quality images and video (these surface separately in AI responses)
- Good page experience and crawlability
- Semantic HTML helps (but perfect code is not required)

**What does NOT matter for Google AI — do NOT recommend these to Google clients:**
- ❌ **llms.txt files** — Google explicitly ignores them; creates no benefit
- ❌ **"Chunking" content** — Google systems understand multi-topic pages; no chunking needed
- ❌ **Rewriting content specifically for AI phrasing** — Google understands synonyms and intent
- ❌ **Seeking inauthentic mentions** — treated as spam signals, not citation signals
- ❌ **Over-focusing on structured data for AI** — schema markup is not required for AI Overviews; continue using it for rich results only

> ⚠️ These "don'ts" apply **exclusively to Google**. For Perplexity, ChatGPT, and Claude, structured data, chunking, and citation-style mentions may still be beneficial.

---

## Phase 3 — Answer Density Check

- Identify the core question the target query implies
- Check if the content answers it directly within the first 60 words
- If not: write a **Direct Answer Paragraph** (40–60 words) to place immediately after the H1
- The Direct Answer Paragraph must: (a) answer the question completely, (b) include the primary keyword naturally, (c) avoid filler phrases like "In this article..."

---

## Phase 4 — Structure Optimization

Convert content to AI-readable formats:

- Rewrite dense prose into structured sections with clear H2/H3 headings
- Match headings to **People Also Ask** and related query variants
- Convert appropriate paragraphs to: numbered lists, comparison tables, definition lists
- Ensure every section opens with a clear topic sentence (the claim, not the buildup)
- Add a **TL;DR** or **Key Takeaways** block near the top (3–5 bullet points, each ≤20 words)

---

## Phase 5 — Citation Readiness

Make content easy for AI systems to extract and quote:

- **Bold** key terms on first definition
- Add specific numbers and data points wherever claims are vague (e.g. "studies show" → "a 2023 Stanford study of 4,200 users found...")
- Include source attributions that AI can reference inline
- Add a **FAQ section** with 3–5 Q&A pairs matching common query variations
- Keep individual paragraphs under 80 words — AI systems prefer extractable chunks

---

## Phase 6 — Entity Optimization

- List the core entities (people, companies, concepts, locations) in the content
- Ensure each entity is clearly defined on first mention
- Cross-reference related entities to build semantic depth
- Add entity context that helps AI systems understand relationships (e.g. "Perplexity, the AI-powered search engine founded in 2022...")

---

## Phase 7 — Language Rules

- **Swiss clients (Schweiz):** Always use `ss` instead of `ß` — no exceptions
- **All German content:** Use correct formal/informal register per tone agreed in Phase 1
- Maintain the original language throughout — do not switch languages mid-output

---

## Output Format

Deliver all four sections in order:

### 1. Direct Answer Paragraph
The 40–60 word answer block to insert after the H1. Label it clearly so the
user can copy-paste it.

### 2. Restructured Content
Full optimized version with all Phase 3–6 changes applied. Use the same
language as the input. Include the TL;DR block and FAQ section.

### 3. Before / After Comparison
Show exactly 2–3 specific sections that changed significantly. For each:
- **Before:** original text
- **After:** optimized text
- **Why:** one sentence explaining the AEO improvement

### 4. AEO Score
Rate both versions on a 1–10 scale across four dimensions:

| Dimension | Original | Optimized |
|---|---|---|
| Answer Density | x/10 | x/10 |
| Structure Clarity | x/10 | x/10 |
| Citation Readiness | x/10 | x/10 |
| Entity Depth | x/10 | x/10 |
| **Overall** | **x/10** | **x/10** |

Include 1–2 sentences on what would push the optimized score even higher.
