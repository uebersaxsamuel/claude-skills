---
name: landing-page-sales-copy-writer
description: >
  Writes high-converting landing page copy with a single clear conversion goal,
  one target audience, and proven StoryBrand structure. Always trigger when the
  user wants to create or improve a landing page, sales page, opt-in page, lead
  page, or homepage — even if they just say "I need a page for my offer", "write
  me a page that sells", "create a landing page for [product/service]", "help me
  write a landing page", "I want more leads", or "my page isn't converting".
  Proactively trigger whenever conversion goals, CTAs, hero copy, headline
  optimization, or "write a homepage" are mentioned. Always ask if SEO is
  relevant — if yes, also activate the seo-aeo-content-writer skill in parallel.
---

# Landing Page Sales Copy Writer

Writes high-converting landing pages using StoryBrand structure, a single
clear conversion goal, and one target audience. No filler content —
every line must serve the one goal.

> **Reference:** For the StoryBrand framework → read `references/storybrand.md`
> For trust elements & conversion best practices → read `references/conversion.md`

---

## Phase 1 — Mandatory Intake (always ask first)

**Ask all of these in a single message before writing anything:**

### Required Questions
1. **Conversion Goal** — What should the visitor DO? (Sale / Lead / Form Signup / Watch Video / Book Demo / Download) → **Only 1 goal per page!**
2. **Target Audience** — Who is the ONE person this page speaks to? Their pain, desire, and context
3. **Offer** — What is being offered? Describe it like you're telling a friend
4. **Tone of Voice** — Formal / Casual / Direct / Empathetic / Premium / Technical
5. **Market / Language** — DE / AT / CH / USA / UK / other
6. **Is SEO relevant?** — Should this page also rank organically?
   - If **Yes** → Write StoryBrand copy AND activate `seo-aeo-content-writer` skill in parallel
   - If **No** → Pure conversion copy without SEO compromises

### Nice to Have
- Existing page / URL to analyze (use `web_fetch`)
- Key trust elements available (testimonials, numbers, certifications, badges)
- Main objections of the target audience
- Biggest competitor (for positioning)
- Current conversion rate / problem with existing page

---

## Phase 2 — Strategy & StoryBrand Positioning

Before writing, define the strategy using the **StoryBrand principle**:

> Read `references/storybrand.md` for the full framework

**Core Principle:** The customer is the hero — NOT the company.
The company is the Guide (like Gandalf, not Frodo).

### StoryBrand Checklist (internal — do not output to user)
- [ ] Who is the Hero? (customer, not brand)
- [ ] What does the Hero want? (external goal)
- [ ] What is the real problem? (internal: frustration/fear, external: symptom, philosophical: "This is wrong")
- [ ] Who is the Guide? (brand as experienced helper, not main character)
- [ ] What is the Plan? (3 simple steps to success)
- [ ] What is the CTA? (direct CTA = "Buy now"; transitional CTA = "Learn more")
- [ ] What are the Stakes? (show both failure and success outcomes)

### Define the Page Strategy
```
CONVERSION GOAL:   [Sale / Lead / Signup / etc.]
TARGET AUDIENCE:   [1 person, 1 pain]
CORE PROMISE:      [What changes after the purchase/signup?]
PRIMARY CTA:       [Only 1 button text, consistent throughout the page]
NAVIGATION:        [Keep minimal — max. 1-2 links + CTA]
SEO KEYWORD:       [Only if SEO = Yes]
```

---

## Phase 3 — Landing Page Structure

Build the page using this proven structure.
**Adjust based on conversion goal** (short lead page vs. long sales page).

### 1. Navigation (Keep Minimal!)
- Logo
- Maximum 1-2 links (e.g. "FAQ" or "About") — or remove entirely
- **1 single CTA button** — same text as the primary CTA on the page

### 2. Hero Section (Above the Fold)
Most important: visitor must understand what they get within 5 seconds.

**StoryBrand Hero Formula:**
```
HEADLINE:    What does the hero's life look like after your offer?
SUBHEADLINE: How you achieve this + who it's for
CTA BUTTON:  [Direct CTA — never "Learn More" here]
```

**Writing Principle:** No "We are XY and we offer..." — go straight to the customer benefit.

### 3. Problem / Pain (Stakes)
- Name the pain explicitly — external, internal, philosophical
- Show that you understand the customer (empathy → authority)
- "If you... [pain], you're in the right place"

### 4. Guide Section — Empathy & Authority
- Position the brand as Guide: "We know this problem because..."
- Brief credibility: numbers, clients, years of experience
- **Not**: "We are the best agency in the world" — instead: "We've helped X achieve Y"

### 5. The Plan (3 Steps)
Make the next step simple and clear:
```
Step 1: [Simple action] → e.g. "Fill out the form"
Step 2: [What happens next] → e.g. "We get back to you within 24h"
Step 3: [Success] → e.g. "You grow / save / win"
```

### 6. Offer Details / Features & Benefits
- **Benefits first, features second**
- "You get..." instead of "The product includes..."
- Every bullet → concrete benefit for the hero

### 7. Trust Section
> Read `references/conversion.md` for detailed trust elements

At least 2 of the following:
- **Testimonials** — with name, photo, specific result (no generic statements)
- **Logos** — known clients, partners, media
- **Numbers** — "500+ clients", "4.9 stars", "since 2018"
- **Badges** — certifications, awards, seals, guarantees
- **Case Studies** — before/after with concrete results

### 8. CTA Section (Repeat the Main Goal)
- Briefly restate the promise
- Direct CTA button (same text as above)
- Show what happens AFTER clicking (reduces anxiety)

### 9. FAQ (Optional but Recommended)
- Answer the 3-5 most common objections
- Write from the customer's perspective: "I'm not sure if..."

### 10. Footer (Minimal)
- Legal / Privacy notice (required for DE/AT/CH; good practice everywhere)
- No additional content that distracts

---

## Phase 4 — Writing the Copy

### Writing Rules
- **Shorter sentences** than in a blog post — readers scan pages
- **Consistent "you/your"** tone throughout
- **Active voice** — "You get" not "It will be provided"
- **Be specific** — "37% more revenue" beats "more revenue"
- **1 goal, 1 CTA text** — identical everywhere on the page
- **No generic filler** — "Welcome to our website" → delete immediately

### StoryBrand Headline Formulas
```
[Who you are] for [audience] — without [biggest pain]
Finally [desired result] — even if [biggest excuse]
How [audience] achieves [result] in [timeframe] [without sacrifice]
[Result] for [audience] — [your method / your promise]
```

### CTA Button Text (never "Submit" or "Click Here")
```
✅ Start for free
✅ Claim my offer
✅ Book a free demo
✅ Get access now
✅ Start [achieving goal]
❌ Submit
❌ Next
❌ Click here
```

---

## Phase 5 — Output Format

Always deliver as a **complete copy document**, structured by section:

```
# Landing Page: [Title]

## Meta
Conversion Goal: ...
Target Audience: ...
Primary CTA: ...
Tone: ...
SEO: Yes / No

---

## NAVIGATION
[Nav copy]

## HERO
Headline: ...
Subheadline: ...
CTA: ...

## PROBLEM
[Copy]

## GUIDE
[Copy]

## PLAN
Step 1: ...
Step 2: ...
Step 3: ...

## OFFER / BENEFITS
[Copy]

## TRUST
[Testimonials / Badges / Numbers]

## CTA SECTION
[Copy + Button]

## FAQ
[Q&A]

## FOOTER
[Minimal]
```

---

## Phase 6 — Final Checklist

Always deliver this checklist at the end of every output:

### ✅ Landing Page Conversion Checklist

**Strategy**
- [ ] Only 1 conversion goal defined
- [ ] Only 1 target audience addressed
- [ ] StoryBrand: customer is hero, brand is guide
- [ ] Clarity: visitor understands what they get within 5 seconds

**Copy**
- [ ] Headline addresses customer benefit (not company feature)
- [ ] Pain/problem clearly named and empathetically handled
- [ ] 3-step plan included
- [ ] CTA text is concrete and action-oriented
- [ ] Same CTA text used consistently throughout the page

**Trust**
- [ ] Min. 2 trust elements present (testimonials, logos, numbers, badges)
- [ ] Testimonials are specific with results (not: "Great service!")
- [ ] Guide's credibility feels genuine and earned

**Design Notes (for Webflow / implementation)**
- [ ] Navigation minimal (max. 1-2 links + CTA)
- [ ] No distracting external links in the hero
- [ ] Mobile hero works without scrolling
- [ ] CTA button visually dominant (color, size)

**SEO (only if relevant)**
- [ ] seo-aeo-content-writer skill was activated
- [ ] Primary keyword in headline / meta title
- [ ] Meta description is conversion-oriented AND keyword-relevant

---

## Non-Negotiable Rules

1. **Never** start writing before Phase 1 is complete
2. **Always** ask about SEO relevance
3. **Always** deliver the checklist at the end
4. If user provides a URL → use `web_fetch` to analyze the existing page first
5. If SEO = Yes → explicitly mention and activate the `seo-aeo-content-writer` skill
6. **Never** allow more than 1 goal per page — if user mentions multiple goals, ask which one to prioritize
