# SEO Audit Reference: Benchmarks & Thresholds

## Title Tag
- Optimal length: 50–60 characters
- Truncation point in Google SERP: ~600px (~60 chars avg)
- Keyword position: ideally within first 30 characters

## Meta Description
- Optimal length: 120–160 characters
- Mobile truncation: ~120 characters
- Required elements: primary keyword, unique value prop, CTA verb

## Heading Structure
- One H1 per page (strictly enforced)
- H2s: major sections, secondary keywords
- No skipping levels (H1 → H3 without H2 is invalid)

## Word Count Benchmarks by Intent
- Informational / how-to: 1,200–2,500 words
- Commercial / comparison: 800–1,500 words
- Transactional / product page: 300–800 words
- Local landing page: 500–1,000 words

## Core Web Vitals Thresholds (Google)
| Metric | Good | Needs Improvement | Poor |
|--------|------|-------------------|------|
| LCP (Largest Contentful Paint) | ≤ 2.5s | 2.5–4.0s | > 4.0s |
| INP (Interaction to Next Paint) | ≤ 200ms | 200–500ms | > 500ms |
| CLS (Cumulative Layout Shift) | ≤ 0.1 | 0.1–0.25 | > 0.25 |

## Image Optimization
- Preferred formats: WebP (broad support), AVIF (cutting edge)
- Alt text: descriptive, keyword-relevant, under 125 chars
- All images need explicit width + height attributes (CLS prevention)
- Lazy loading: all below-fold images should have loading="lazy"

## Hreflang
- Always include x-default pointing to canonical fallback
- Hreflang must be reciprocal (A links to B, B must link back to A)

## E-E-A-T Signals Checklist
- [ ] Author byline with credentials
- [ ] Author bio page with expertise indicators
- [ ] Publication/update date visible
- [ ] Citations to primary sources (gov, academic, industry)
- [ ] First-person experience language ("In our testing...", "We found...")
- [ ] Clear contact information / About page
- [ ] Privacy policy and legal pages linked from footer

## Robots Meta Directives
- `index, follow` — Default, no tag needed
- `noindex, follow` — Exclude from index, still crawl links
- `index, nofollow` — Index page, don't pass link equity
- `noindex, nofollow` — Full exclusion (use sparingly)

## Redirect Rules
- 301: Permanent redirect (passes ~90–99% link equity)
- 302: Temporary redirect (does NOT pass link equity long-term)
- Redirect chains over 2 hops should be flattened
- Redirect loops = CRITICAL issue
