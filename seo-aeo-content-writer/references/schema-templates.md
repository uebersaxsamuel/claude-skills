# Schema Markup Templates

Ready-to-use JSON-LD snippets. Copy, fill placeholders, and add to page `<head>`.

---

## Article / BlogPosting

```json
{
  "@context": "https://schema.org",
  "@type": "BlogPosting",
  "headline": "TITLE",
  "description": "META_DESCRIPTION",
  "author": {
    "@type": "Person",
    "name": "AUTHOR_NAME",
    "url": "AUTHOR_URL"
  },
  "publisher": {
    "@type": "Organization",
    "name": "COMPANY_NAME",
    "url": "SITE_URL",
    "logo": {
      "@type": "ImageObject",
      "url": "LOGO_URL"
    }
  },
  "datePublished": "YYYY-MM-DD",
  "dateModified": "YYYY-MM-DD",
  "image": "OG_IMAGE_URL",
  "url": "CANONICAL_URL",
  "inLanguage": "de-CH"
}
```

---

## FAQPage

```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "QUESTION_1",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "ANSWER_1"
      }
    },
    {
      "@type": "Question",
      "name": "QUESTION_2",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "ANSWER_2"
      }
    }
  ]
}
```

Add one object per FAQ pair. Max 10 for Google display.

---

## Service + LocalBusiness (Webflow agency / consultant use case)

```json
{
  "@context": "https://schema.org",
  "@type": ["LocalBusiness", "ProfessionalService"],
  "name": "COMPANY_NAME",
  "url": "SITE_URL",
  "telephone": "PHONE",
  "email": "EMAIL",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "STREET",
    "addressLocality": "CITY",
    "postalCode": "ZIP",
    "addressCountry": "CH"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": LAT,
    "longitude": LNG
  },
  "areaServed": ["CH", "DE", "AT"],
  "hasOfferCatalog": {
    "@type": "OfferCatalog",
    "name": "Services",
    "itemListElement": [
      {
        "@type": "Offer",
        "itemOffered": {
          "@type": "Service",
          "name": "SERVICE_NAME",
          "description": "SERVICE_DESCRIPTION"
        }
      }
    ]
  }
}
```

---

## HowTo

```json
{
  "@context": "https://schema.org",
  "@type": "HowTo",
  "name": "HOW_TO_TITLE",
  "description": "HOW_TO_DESCRIPTION",
  "totalTime": "PT30M",
  "step": [
    {
      "@type": "HowToStep",
      "name": "STEP_1_NAME",
      "text": "STEP_1_DESCRIPTION",
      "position": 1
    },
    {
      "@type": "HowToStep",
      "name": "STEP_2_NAME",
      "text": "STEP_2_DESCRIPTION",
      "position": 2
    }
  ]
}
```

---

## BreadcrumbList (recommended on all pages)

```json
{
  "@context": "https://schema.org",
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
      "name": "ARTICLE_TITLE",
      "item": "ARTICLE_URL"
    }
  ]
}
```

---

## Combining Multiple Schemas

Use `@graph` to combine multiple schemas on one page:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    { ...BlogPosting schema... },
    { ...FAQPage schema... },
    { ...BreadcrumbList schema... }
  ]
}
```

This is best practice for blog posts with FAQs.
