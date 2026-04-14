# Otterly Booked — Marketing Site

Single-page marketing site for [otterlybooked.com](https://otterlybooked.com). Pricing intelligence consultancy for independent UK hotels (20–150 rooms).

Static HTML, no build step, no framework. Deploy by dropping the repo onto any static host.

## Structure

```
otterly-booked-site/
├── index.html       # Entire site — HTML, embedded CSS, embedded JS
├── images/          # Headshots, OG image, favicons (add as needed)
└── README.md
```

That's it. One file does everything.

## Local preview

Open `index.html` in a browser. Or, for proper relative-path behaviour:

```bash
# Python
python -m http.server 8000

# Node
npx serve .
```

Then visit `http://localhost:8000`.

## Deploying to Netlify

Netlify will deploy this site for free with HTTPS, global CDN, and atomic deploys.

1. **Push this repo to GitHub** (see *Initial GitHub setup* below).
2. **Sign in to [app.netlify.com](https://app.netlify.com)** and click **Add new site → Import an existing project**.
3. **Connect to GitHub** and select `otterly-booked-site`.
4. **Build settings:**
   - Build command: *(leave blank)*
   - Publish directory: `.` *(or leave blank — repo root)*
5. Click **Deploy site**. First deploy takes ~30 seconds. Netlify will give you a temporary URL like `https://gleaming-otter-abc123.netlify.app`.
6. Every push to `main` triggers a new deploy automatically. Pull requests get preview URLs.

### Custom domain (otterlybooked.com)

In Netlify:

1. Go to **Site settings → Domain management → Add custom domain**.
2. Enter `otterlybooked.com`. Netlify will also offer to add `www.otterlybooked.com` — accept both.
3. Netlify will show you DNS records to set. You'll need them for the next step.

In Namecheap (Domain List → Manage → Advanced DNS):

1. Delete any existing `A`, `CNAME`, or `URL Redirect` records for `@` and `www`.
2. Add these records (Netlify will show the exact values — these are the typical ones):

   | Type | Host | Value | TTL |
   |------|------|-------|-----|
   | `A` | `@` | `75.2.60.5` *(Netlify's load balancer)* | Automatic |
   | `CNAME` | `www` | `<your-site>.netlify.app` | Automatic |

   Alternative: point the apex to Netlify DNS (more reliable, requires changing nameservers in Namecheap → Domain → Nameservers).

3. DNS propagation: usually 5–30 minutes, sometimes a few hours.

### HTTPS

Once DNS propagates, Netlify will automatically provision a Let's Encrypt certificate. No action needed. Force HTTPS in **Domain management → HTTPS → Force HTTPS**.

## Editing

It's one file. Open `index.html` in any editor.

- **Copy:** look for the section comment markers (`<!-- ============ HERO ============ -->` etc.).
- **Colours / fonts:** all design tokens are in the `:root` block at the top of `<style>`.
- **ROI calculator logic:** at the bottom of `<script>`, function `calc()`. Uplift assumptions live on the `<select id="approach">` options as the `value` attribute.
- **Headshots:** drop files in `/images/` and replace the `.avatar` divs in the About section with `<img>` tags.

## Initial GitHub setup

The local repo is already initialised and has its initial commit. After creating an empty repo at [github.com/nathannoerr/otterly-booked-site](https://github.com/new) (don't tick "Initialize with README"), wire up the remote and push:

```bash
git remote add origin https://github.com/nathannoerr/otterly-booked-site.git
git push -u origin main
```
