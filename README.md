# BreathEZs — Shopify deploy branch (`shopify-live`)

**This branch is the live Shopify theme, with theme files at the repo root so
Shopify's *Connect from GitHub* can sync it.** Every commit here auto-updates
the connected store theme.

- **Do NOT edit this branch by hand, and do NOT edit in the Shopify theme editor.**
  It is generated from `index.html` on the `claude/shopify-integration-aeihzx`
  branch. Editing in Shopify would sync edits back here and diverge from source.
- To change the site: edit `index.html` on the source branch, regenerate the
  theme, and update this branch.

## Connect it in Shopify
Online Store → Themes → Add theme → **Connect from GitHub** → repo
`lumentrail/breathezs`, branch `shopify-live` → then **Publish**.
