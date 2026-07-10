# BreathEZs marketing site — working notes

Single-file static marketing site (`index.html`) for BreathEZs® (BEZ), a premium
100% cotton underwear brand with an open-rear airflow design. Lives at
breathezs.com. No build step; assets in `images/`, `videos/`, `fonts/`
(self-hosted Poppins + Great Vibes). Work on branch
`claude/breathezs-website-analysis-1kgs8i`.

## Live preview artifact
https://claude.ai/code/artifact/16d6272d-2a81-4ba9-9bc5-954e8493d9c2
To refresh it: inline all assets (fonts, `url(images/...)`, `src="images/..."`,
`data-*="images/..."`, `src="videos/..."`) as base64 data URIs into a single
HTML file and publish it to that URL with the Artifact tool.

## Brand rules (owner: Mike; founder: Rich White — never "Ricky")
- Inclusive positioning: all genders/orientations; avoid "men's underwear" copy.
- Field Tested testimonials must be real third parties — never quotes from Rich.
- Tagline "No Heat For Your Meat.™" is wanted (gold, in the night section).
- Avoid the word "invisible" in claims (use "discreet"); no em-dashes in copy.
- Launch: August 2026 (preorder soft launch). Contact: customerservice@breathezs.com.
- Palette purple-forward with gold accents; font Poppins everywhere; cursive
  accents in Great Vibes. Hero background base color is #0a0810.

## Layout facts
- Hero: neon BEZ sign image `images/hero-neon.jpg` pinned right at
  `auto 100%`; background must exactly match #0a0810 (no CSS filters on it —
  filters caused a visible box seam). Mobile hero uses `images/bez-neon.jpg`.
- Collection: one "Classic" card with white/black color selector (front/back
  images swap; always reset to front on color change) + Special Edition card.
  Cards flip front/back on hover (desktop, image-only hover) and tap (mobile).
- Product photos are processed to 4:5, subject filling the frame, no hangers.
- Night section: `videos/special-edition-promo.mp4` — cleaned AI clip
  (boomerang sweep; source has a hard cut at frame ~326 and the box warps
  edge-on, so a true 360 is impossible from this source). Caption strip above
  the video hides nothing; the scrim over the video top hides a garbled
  baked-in title. Small BEZ logo bug bottom-right.
- Shop links scroll to #collection for now; `STORE_URL` constant + `store-link`
  class exist for the future Shopify (Liquid) integration.

## Open items
1. Waitlist forms only save to localStorage — wire Mailchimp/Klaviyo before launch.
2. Replace the Special Edition clip when Mike generates a better one (prompt
   given: black brief + purple emblem + collector box, slow 360 turntable,
   dark purple neon set, photoreal, no text, no people, no camera movement,
   perfect loop). Clean/loop/integrate it.
3. Shopify conversion when the storefront is finalized.
