## Pages
- Create: input textarea/URL field, template picker (3 thumbnails), color pickers, font dropdown, logo uploader URL, tagline input, Generate button, preview repeating group for images, Download PNGs/PDF buttons.
- Account/Billing: login/signup, plan selection, Stripe subscription component, usage meter.
- Dashboard: list of previous Carousels.

## Workflows
- Generate button → Create Carousel (draft) → call Make webhook with form values → set status=rendering.
- When webhook response received (API Connector), update Carousel.imageUrls, pdfUrl, status=ready.
- Download buttons: open file URLs.
- Gating: before calling webhook, check User.plan quota vs monthlyUsage.

## Gating rules
- Free: 3/month; Pro: 30/month; Unlimited: no cap.
- On successful render (status=ready), increment User.monthlyUsage.
- Monthly reset: backend workflow (scheduled every 1st of month) sets monthlyUsage=0 for all users.

## Template picker
- Store `templateKey` in Carousel from radio buttons: modern, bold, minimal.
- Show static previews (exported PNGs) next to choices.

## API Connector (Bubble)
- Endpoint: Make webhook URL
- Method: POST JSON, send all fields from payload schema
- Response: map imageUrls (list) and pdfUrl to Carousel