# Project: Amalphia Sylva belly dance class website

A finished static website (plain HTML and CSS, no build step) for belly dance classes in Biscoe, North Carolina. The deployable site is the `site/` folder. Design came from a mockup made in a Claude.ai session; do not redesign it unless asked.

## Goal
Publish `site/` to Cloudflare Pages (free plan) and connect the owner's custom domain, which is registered at DreamHost. Keep total cost to the domain renewal only.

## Files
- `site/index.html`, `site/styles.css`: the whole site. Fonts load from Google Fonts.
- `site/images/`: optimized photos (all under 500 KB).
- Class times, rates and contact details are in `site/index.html`. Dates are "posted soon" on purpose. Do not invent dates, prices or class times.

## Deploy to Cloudflare Pages
Needs Node.js and npm on this machine. The owner has a Cloudflare account.

1. Ask the owner to create a Cloudflare API token limited to **Account > Cloudflare Pages > Edit** and to set these in their own shell (never in chat, never in a file in this folder, never committed):
   ```
   export CLOUDFLARE_API_TOKEN=...
   export CLOUDFLARE_ACCOUNT_ID=...
   ```
   The account ID is on the Cloudflare dashboard's Workers & Pages overview page. Tell the owner to delete the token when finished.
2. From this folder run:
   ```
   npx wrangler pages deploy site --project-name amalphia-sylva
   ```
   Accept creating the project if asked (production branch: `main`). The site then answers at `https://amalphia-sylva.pages.dev`.
3. Open the URL and check it on a phone-sized window too: hero, class times, prices, email button, video links.
4. Re-run step 2 after any edit. A project made this way cannot be switched to Git later; that is fine.

## Connect the custom domain (registered at DreamHost)
Ask the owner for the domain name first. Ask whether the domain has email or other services through DreamHost. If it has email, list the existing MX/TXT records from DreamHost and copy every one into Cloudflare DNS before changing nameservers, or email will stop working.

Recommended (works for the bare domain and www):
1. Cloudflare dashboard: add the domain as a site on the Free plan. Let it import existing DNS records and compare them against DreamHost's DNS list.
2. In the DreamHost panel, set the domain's nameservers to the two Cloudflare gives. The owner does this step, or signs in and lets Claude click through the browser while they watch.
3. In Cloudflare, Workers & Pages > the project > Custom domains: add the bare domain and `www`. Wait for the certificate to become active.
4. Optional: redirect `www` to the bare domain (or the reverse) with a Cloudflare redirect rule.

Simpler fallback: keep DNS at DreamHost and add one CNAME, `www` to `amalphia-sylva.pages.dev`. Only `www.` works then, not the bare domain.

## Rules
- Never ask for, store or echo passwords or tokens. The owner enters secrets in their own shell or browser.
- Confirm with the owner before changing DNS or nameservers.
- Keep the site static. Sign-ups go by email (mailto buttons); no form backend.
- Photos: the festival photo (`images/festival.jpg`) carries a Phoenix Rising Dance Festival watermark. Ask the owner whether they have permission to use it.

## Open questions for the owner
- Is the beginner fusion course actually running? The page lists it with no separate schedule.
- What is the domain name, and is there DreamHost email on it?
