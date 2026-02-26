# SEO Site Auditor — Eval Test Cases

## Test Case 1: Minimal HTML Page
**Input:**
```
Audit this HTML:
<html>
<head><title>Bread Baking</title></head>
<body><h1>Bread Baking Made Easy</h1><p>Bread baking is great.</p></body>
</html>
Keyword: "easy bread baking recipe"
```
**Expected outputs:**
- CRITICAL: Missing meta description
- CRITICAL: Missing canonical tag
- CRITICAL: Missing viewport meta tag
- WARNING: Title too short / missing keyword suffix
- WARNING: Thin content (under 300 words)
- WARNING: No H2 structure
- OPTIMIZATION: Missing hreflang (if multi-language site)

---

## Test Case 2: Well-Optimized Page
**Input:**
```
Audit this page. It has:
- Title: "Accounting Software for SMEs – Try Free | FibuApp" (50 chars)
- Meta description: "Discover the leading accounting software for small businesses. Try free for 30 days – no credit card required." (110 chars)
- One H1: "Accounting Software for Small Businesses"
- H2s: Features, Pricing, Testimonials, FAQ
- 1,400 words, WebP images with alt text and dimensions, canonical self-referencing
- hreflang: en-US, en-GB, x-default
Keyword: "accounting software SME"
```
**Expected outputs:**
- No CRITICAL issues
- WARNING: Meta description slightly short (110 < 120 chars)
- OPTIMIZATION issues only for minor items
- Audit acknowledges strong hreflang setup

---

## Test Case 3: Multi-Issue Technical Page
**Input:**
```
Audit: page has a 302 redirect to itself, no canonical, images without alt text,
H1 missing, H2 jumps directly to H4, title is 95 characters long,
no viewport tag, render-blocking Google Fonts in <head> without font-display.
Keyword: "project management tool"
```
**Expected outputs:**
- Multiple CRITICAL issues (302 redirect loop, missing H1, no viewport)
- Table sorted CRITICAL first
- Specific fix instructions (not vague)
- Quick Wins identifies the 3 highest-ROI fixes

---

## Scoring Rubric

| Criterion | Weight | Pass Condition |
|-----------|--------|----------------|
| Table format correct (5 columns) | 25% | All 5 columns present in every row |
| Priority sorting (CRITICAL first) | 15% | No WARNING before all CRITICALs |
| Quick Wins section present | 20% | Exactly 3 items, formatted correctly |
| Fix instructions are specific | 25% | Each fix includes exact code or action |
| No false positives on TC2 | 15% | No CRITICAL on well-optimized page |
