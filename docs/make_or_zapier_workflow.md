### Overview
Triggered by Bubble webhook. Steps:
1) Receive payload: { sourceType, sourceInput, templateKey, brand colors, font, logoUrl, brandTagline }
2) If sourceType=url, fetch and extract article text (e.g., Make HTTP Get + Readability or LinkPreview API). Else use sourceInput as text.
3) Call OpenAI API with prompt (docs/openai_prompt.txt) to get slides JSON.
4) For each slide, render image via HTML-to-image service (APITemplate.io/Placid/Bannerbear) using selected template + variables.
5) Zip all PNGs. Optionally, merge into single PDF.
6) Upload files (Make: Cloud storage or Bubble file upload). Return URLs to Bubble via webhook response.

### Input payload (Bubble → webhook)
{
  "carouselId": "bubble-thing-id",
  "sourceType": "text|url|idea",
  "sourceInput": "...",
  "templateKey": "modern|bold|minimal",
  "brandPrimary": "#6C5CE7",
  "brandAccent": "#00CEC9",
  "brandBg": "#0f1020",
  "fontFamily": "Inter",
  "logoUrl": "https://.../logo.png",
  "brandTagline": "@yourbrand"
}

### OpenAI (Make: OpenAI > Create a completion/chat)
- Model: gpt-4o-mini (or gpt-4o)
- Temperature: 0.7
- System: empty or brief persona
- User content: prepend contents of docs/openai_prompt.txt + two newlines + source text
- Parse response as JSON array of slides

### Rendering (APITemplate.io as example)
- Create a template for each of the 3 HTML files in `/templates/`.
- Variables per slide call:
  - slide_title → slides[i].slideTitle
  - bullet_1..3 → slides[i].bulletPoints[0..2]
  - slide_number → i+1
  - total_slides → slides.length
  - brand_primary, brand_accent, brand_bg, font_family, logo_url, brand_tagline
- API: POST /v1/create?template_id=... (per service docs)
- Collect returned imageUrl into array

### Zip and PDF
- Make: Tools > Archive a file (ZIP) from list of files/urls
- PDF options:
  - CloudConvert: images → merged PDF
  - APITemplate: multi-page PDF if supported

### Response (webhook → Bubble)
{
  "carouselId": "...",
  "imageUrls": ["https://.../1.png", "https://.../2.png", ...],
  "pdfUrl": "https://.../deck.pdf"
}

### Error handling
- If OpenAI or rendering fails, respond with status=failed and error message.
- Bubble workflow sets Carousel.status accordingly.