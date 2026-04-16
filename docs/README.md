# Artic.le — Legal Documents

Privacy Policy, Terms of Service, and Data Deletion Instructions for Artic.le.

## Structure

```
/
├── index.html                        # Language picker landing page
├── styles.css                        # Shared styles
├── en/
│   ├── privacy-policy.html
│   ├── terms-of-service.html
│   └── data-deletion.html
└── pt/
    ├── politica-de-privacidade.html
    ├── termos-de-uso.html
    └── exclusao-de-dados.html
```

## The three URLs Facebook requires

After hosting (see options below), these are the URLs you'll paste into Facebook's app settings:

- **Privacy Policy URL:** `https://<your-host>/en/privacy-policy.html`
- **Terms of Service URL:** `https://<your-host>/en/terms-of-service.html`
- **User Data Deletion URL:** `https://<your-host>/en/data-deletion.html`

Facebook reviewers default to English. Use the English URLs even though you also serve Portuguese — the Portuguese versions are discoverable via the language links in the footer.

## Hosting Option 1 — GitHub Pages (recommended for v1)

1. Create a new public GitHub repo, e.g. `articulate-legal` (name is up to you; keep it simple).
2. Copy the contents of this folder into the repo root.
3. Commit and push.
4. In the repo settings, go to **Pages** → **Source** → select the `main` branch and `/ (root)` folder. Save.
5. Wait ~60 seconds for GitHub to build the site.
6. Your URLs will be:
   - `https://<your-github-username>.github.io/articulate-legal/en/privacy-policy.html`
   - `https://<your-github-username>.github.io/articulate-legal/en/terms-of-service.html`
   - `https://<your-github-username>.github.io/articulate-legal/en/data-deletion.html`

That's it. GitHub Pages is free, auto-renews HTTPS, and gives you version history on every edit.

### Optional: custom domain later

When you have your marketing site domain set up (e.g. `artic.le`), you can point a subdomain like `legal.artic.le` at GitHub Pages:

1. Add a `CNAME` file to the repo root containing your domain: `legal.artic.le`.
2. In your DNS, add a CNAME record `legal.artic.le → <your-github-username>.github.io`.
3. In GitHub Pages settings, enter the custom domain and enable "Enforce HTTPS."
4. Update the URLs in your Facebook app settings.

## Hosting Option 2 — Cloudflare R2 with a custom domain

If you already have Cloudflare and an R2 bucket, you can host these files there:

1. Upload all six HTML files + `styles.css` to an R2 bucket named e.g. `articulate-legal`.
2. Make the bucket public.
3. Bind the bucket to a custom domain in the R2 dashboard (e.g. `legal.artic.le`).
4. URLs will be `https://legal.artic.le/en/privacy-policy.html` etc.

R2 has no egress fees, which matters if these pages ever get hit hard. For a solo dev's legal pages, though, GitHub Pages is simpler.

## Hosting Option 3 — Your marketing site, later

When you build a marketing site for Artic.le (Next.js on Vercel, Astro on Netlify, etc.), move these pages in as `/privacy`, `/terms`, `/data-deletion`, `/pt/privacy`, `/pt/terms`, `/pt/data-deletion`. This is the ideal long-term home — same domain as the brand, full control, and it signals legitimacy to reviewers at Apple/Google/Facebook.

The pages are self-contained (single HTML + one CSS file), so moving them to any static-site framework is a matter of copy/paste.

## Before you submit to Facebook — 10-point checklist

1. **Verify `diogodow@gmail.com`** forwards to an inbox you check. Reviewers test these.
2. **Verify all three URLs return HTTP 200** when opened in an incognito browser window. No 404s, no redirects to a login page, no "site under construction."
3. **The data deletion page must be reachable from the privacy policy** — I already linked them cross-wise in both language sets.
4. **Visit each URL from your phone** — Facebook reviewers frequently use mobile. The pages are responsive, but check for yourself.
5. **Make sure the page title and `<h1>` both clearly say "Privacy Policy" / "Terms of Service" / "Data Deletion"** — reviewers run automated checks.
6. **If you list a company or address** — keep it real. If it's just you as a solo developer in Brazil, say that (the template says "an independent developer based in Brazil"). Do not invent a company name.
7. **If you plan to use Google or Facebook signup** — the Privacy Policy must mention this by name. Mine does.
8. **Set up the Data Deletion Callback URL on your backend** — this is separate from the data-deletion *instructions* page. It's a webhook at something like `https://api.artic.le/v1/auth/facebook/data-deletion` that Facebook calls when a user deletes your app from their Facebook. The callback is handled by Facebook's Platform Terms (required for any Facebook Login integration).
9. **Before submission, open the Privacy Policy URL in an incognito window and run Google Lighthouse** — Facebook's automated checks look at load time and accessibility. These pages score near-100 out of the box, but worth verifying.
10. **Keep a copy of the version you submitted.** If you change the policy later, you want to be able to point to what was live at a given date. GitHub Pages gives you this for free via commit history.

## When content needs updating

Legal docs age quickly. Revisit them whenever you:

- Add a new third-party integration (new LLM provider, new analytics tool, new auth method).
- Start charging for a feature (adds payment processor to data sharing).
- Expand to a new country with different data laws (e.g., California CCPA, if you start marketing there).
- Change what data you collect (new events tracked, new opt-in features).

At minimum, update the "Last updated" date and review the content every 6 months.

## A sincere disclaimer

These documents are a solid starting baseline that will pass Facebook review and give you reasonable LGPD coverage for a solo-dev app. They are **not** a substitute for advice from a Brazilian data protection lawyer, especially before you:

- Start collecting payment information.
- Scale to thousands of daily active users.
- Add features that could be considered "sensitive data processing" under LGPD (biometrics, health, political opinions, etc.).

A one-hour consultation with a Brazilian lawyer specializing in LGPD typically runs R$ 300–R$ 800 and is worth it before you hit any of those milestones.

## Questions

If you need to modify the content, the HTML is straightforward. Each section has a clear `<h2>` and `<h3>` structure, and the styling is driven by CSS variables in `styles.css` that match the Artic.le brand tokens (glacial cyan accents, dark mode support, etc.).
