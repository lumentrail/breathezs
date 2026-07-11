# Getting BreathEZs live on Shopify (marketing site, pre-launch)

This puts the BreathEZs marketing site online as your Shopify store's
homepage — **no products or checkout yet**. People can learn about the
product now; we wire up the actual buy capability later.

The converted theme lives in [`shopify-theme/`](shopify-theme/). The
ready-to-upload **`breathezs-shopify-theme.zip`** is sent to you directly
(it's a build artifact, regenerated from `shopify-theme/`, not committed to
git). To rebuild it yourself: `cd shopify-theme && zip -rq ../breathezs-shopify-theme.zip .`

## What this is

The single-file marketing site (`index.html`) converted into a valid
Shopify (Liquid) theme:

- `layout/theme.liquid` — the page `<head>`, all CSS, and the required
  Shopify `content_for_header` / `content_for_layout` hooks.
- `templates/index.liquid` — the full marketing page (hero, technology,
  collection, night section, waitlist, FAQ, footer) as the store homepage.
- `assets/` — every image, video, and font (Shopify's assets folder is
  flat, so they were flattened and all references rewritten to
  `{{ '…' | asset_url }}`).
- Light stub templates for the other storefront routes (404, cart,
  product, etc.) so nothing errors before launch.
- `config/` + `locales/` — the required theme metadata.

The static `index.html` in this repo is **untouched** and still works on its own.

## Step 1 — Create a Shopify store (you)

1. Go to <https://www.shopify.com> and start a store (a trial is fine to
   begin; a paid plan is required before you can actually sell later).
2. Pick your `*.myshopify.com` handle.
3. You do **not** need to add products, payments, or shipping for this
   marketing launch.

## Step 2 — Upload the theme

1. In Shopify admin: **Online Store → Themes**.
2. Scroll to the bottom → **Add theme → Upload zip file**.
3. Upload **`breathezs-shopify-theme.zip`** (sent to you in chat; or rebuild
   it with the command above).
4. Once it appears in the theme list, click **Actions → Publish**.

## Step 3 — Make the site public

By default a new store is password-protected. To let people see it:

- **Online Store → Preferences → Password protection → uncheck** "Restrict
  access to visitors with the password."
- (If you'd rather keep it locked with a teaser, leave it on — the theme
  includes a branded password page.)

## Step 4 — Point breathezs.com at Shopify (optional, recommended)

- **Settings → Domains → Connect existing domain** → `breathezs.com`, then
  follow Shopify's DNS instructions with your registrar.

## After launch — adding the buy capability (later)

The store seam is already in the theme, so turning on purchases is a small change:

- `STORE_URL` constant and the `store-link` class already exist in
  `templates/index.liquid`. When products are ready, tag the "Shop" buttons
  with `class="store-link"` and set `STORE_URL`, or upgrade to Shopify's
  Buy Button SDK / native product pages.

## Still open before selling

- Waitlist form currently saves to the browser only (`localStorage`) — wire
  it to Mailchimp/Klaviyo (or a Shopify customer/marketing signup) before launch.
- Add real products, prices, payments, and shipping when the storefront is finalized.

## Re-generating the theme

If `index.html` changes, the theme is rebuilt by the same conversion:
head/body split + rewriting `images/` `videos/` `fonts/` references to
`{{ '…' | asset_url }}`, with all assets flattened into `assets/`.
