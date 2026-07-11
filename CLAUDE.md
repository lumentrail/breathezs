# BreathEZs — project handoff & working notes

BreathEZs® (BEZ) is a premium 100% cotton underwear brand with an open-rear
airflow design. This repo is the marketing site, converted into a **Shopify
Liquid theme**. Status: pre-launch, soft launch (preorders) targeted for
**August 2026**. Live domain when connected: **breathezs.com**.
Contact: customerservice@breathezs.com. Founder: **Rich White**.

> New session / new agent? Read this whole file first, then look at
> `templates/index.liquid` (the homepage) and `layout/theme.liquid` (head + all
> CSS). That is 90% of the site.

## Branches — what is what

- **`shopify-live`** — the real, deployed Shopify theme at repo root
  (`layout/`, `templates/`, `assets/`, `config/`, `locales/`). **Edit here to
  change the live site.** Commits here are titled `Deploy: …`.
- **`claude/shopify-integration-aeihzx`** — the theme **source**. Same theme
  but under `shopify-theme/`, plus `SHOPIFY-SETUP.md`. The theme files are
  byte-identical to `shopify-live` aside from the path. **When you change the
  theme, apply the same change to BOTH branches** so a deploy never regresses.
- **`claude/breathezs-website-analysis-1kgs8i`** — **ARCHIVED.** The original
  single-file static `index.html` marketing site. Superseded by the theme; do
  not build features here.
- **`backup/*`** (e.g. `backup/shopify-live-pre-reserve`) — rollback points.
  Restore from these if a change misbehaves.

## Theme structure

- `layout/theme.liquid` — the `<head>`, **all** the CSS (one big `<style>`),
  and Shopify's `content_for_header` / `content_for_layout` hooks.
- `templates/index.liquid` — the entire homepage (hero → FAQ → footer) and the
  page `<script>`.
- `templates/page.privacy-policy.liquid` — Privacy Policy page (`/pages/privacy-policy`).
- `assets/` — flat folder holding every image, video, and font. Reference with
  `{{ 'file.ext' | asset_url }}` (assets are flattened — no subfolders).
- Other `templates/*.liquid` are light stubs so storefront routes don't error
  before launch.

## Key behaviors

- **Reservations:** the "Get In Before They're Gone" section is a native
  Shopify `{% form 'customer' %}` with **Style / Color / Size** dropdowns. On
  submit, JS folds the picks into `contact[tags]` (`style-*`, `color-*`,
  `size-*`) so each reservation lands on the Shopify **customer record**,
  filterable in the Customers tab. Name → `contact[first_name]`. The footer form
  is an email-only newsletter. **No external backend.**
- Product-card "Reserve Yours" buttons preselect that style (and Classic's
  chosen swatch color) and jump to the form. Special Edition locks color to Black.
- **TODO (deferred):** itemized confirmation emails to customerservice@ **and**
  the customer. Native customer capture does not email you the details — wire a
  parallel `{% form 'contact' %}` or a serverless/Zapier endpoint. The seam is
  `RESERVE_ENDPOINT` in `templates/index.liquid`.

## Brand rules (do not break)

- Inclusive: all genders/orientations; avoid "men's underwear" copy.
- Founder is **Rich White** — never "Ricky". No testimonials attributed to Rich.
- Tagline **"No Heat For Your Meat.™"** is wanted (gold accent).
- Avoid the word "invisible" (use "discreet"). No em-dashes in copy.
- Palette purple-forward with gold accents. Poppins everywhere; Great Vibes for
  cursive accents. Hero background base color `#0a0810`.

## Local preview (important limitation)

Shopify Liquid cannot be rendered by a plain static file server. To eyeball
changes locally you must resolve the Liquid (rewrite `{{ '…' | asset_url }}` →
`assets/…`, turn `{% form %}` into a plain `<form>`, strip remaining Liquid) and
serve the result. The **authoritative** preview is Shopify's own theme editor
preview after the theme is uploaded/connected.

## Deploying to Shopify

See `SHOPIFY-SETUP.md` on the source branch. Summary: create a store, then
either upload the theme as a zip **or** connect this repo via Shopify's GitHub
integration, unlock password protection (Online Store → Preferences), and point
breathezs.com under Settings → Domains. Shopify auto-provisions SSL.

## Secrets & access — NEVER commit these

By design, **no credentials live in this repo.** Provide them out-of-band
(environment variables, Shopify app settings) and never in tracked files:

- **GitHub push access** — a personal access token, supplied at runtime.
- **Shopify Storefront/Admin API tokens** — only needed later for products,
  checkout, or a reservation-email backend. Keep them in a serverless env, not here.

If you need a credential, ask the owner. Do not hardcode or commit tokens,
passwords, or `*.myshopify.com` admin secrets.

## Open items / next steps

1. Create the Shopify store; add products (Classic White/Black, Special Edition
   Black) with sizes S–3XL as variants.
2. Connect breathezs.com and turn off password protection.
3. Wire reservation confirmation emails (`RESERVE_ENDPOINT` → serverless /
   Zapier / native `{% form 'contact' %}`).
4. Add real prices, payments, and shipping for actual checkout.
5. Replace the Special Edition promo video with a cleaner loop when available.

## Windows git note

Cloning/pushing on Windows may need `http.sslBackend=schannel` and
`http.schannelCheckRevoke=false` (already set in this clone's config) to avoid
SSL cert / revocation errors.
