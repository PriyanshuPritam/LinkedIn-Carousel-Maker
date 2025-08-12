# LinkedIn Carousel Maker assets

Contents:
- `/templates/`: 3 HTML templates (modern, bold, minimal) at 1080x1080 with Liquid-style variables.
- `/docs/openai_prompt.txt`: copy/paste this into Make/Zapier OpenAI step.
- `/docs/*`: Bubble data model, setup, Make/Zapier workflow, Stripe setup, variable mapping.

Quick start (APITemplate.io):
1) Create a new HTML template, paste one of the files in `/templates/`.
2) Define variables listed in `/docs/variables_mapping.md`.
3) From Make, call the render endpoint per slide, pass variables, collect `imageUrl`.
4) Zip all images, merge to PDF if needed, send URLs back to Bubble.

Tip: Export a cover slide and closing slide too. Use the same templates with different text.