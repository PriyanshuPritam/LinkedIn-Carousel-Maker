## Data types

- User
  - plan (text) — one of: Free, Pro, Unlimited
  - monthlyUsage (number)
  - stripeCustomerId (text)

- Carousel
  - owner (User)
  - sourceType (text) — one of: text, url, idea
  - sourceInput (text)
  - slidesJson (text) — JSON from OpenAI
  - templateKey (text) — e.g., modern, bold, minimal
  - brandPrimary (text)
  - brandAccent (text)
  - brandBg (text)
  - fontFamily (text)
  - logoUrl (text)
  - brandTagline (text)
  - imageUrls (list of text)
  - pdfUrl (text)
  - status (text) — one of: draft, rendering, ready, failed

- Slide (optional; can be derived from JSON)
  - carousel (Carousel)
  - index (number)
  - title (text)
  - bullets (list of text)

## Option sets

- Plan: Free (3), Pro (30), Unlimited (9999)

## Privacy rules (minimal)

- Carousel: owner can read/write, others none
- User: users can read/write own fields, read only plan for self