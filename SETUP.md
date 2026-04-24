# Flying Fish Site — Setup & Deployment Notes

## What Was Built

A single-page author website for *A Fish! A Fish! A Flying Fish!* by Trisha Kunst.

**Stack:** Pure HTML + CSS (no framework, no build step)
**Hosting:** GitHub Pages (free)
**Repo:** https://github.com/tkunst/flying-fish-site
**Live URL:** https://tkunst.github.io/flying-fish-site/

**Files:**
- `index.html` — all page content (one page, four sections)
- `css/style.css` — all styles, colors, animations
- `README.md` — short deployment reference
- `SETUP.md` — this file

---

## How to Make Changes

Edit `index.html` or `css/style.css` locally, then:

```bash
git add .
git commit -m "describe what you changed"
git push
```

GitHub Pages rebuilds automatically within ~60 seconds. Refresh the live URL to see changes.

---

## How to Add a Custom Domain (e.g. flyingfishbook.com)

### Step 1 — Buy the domain

Recommended registrars:
- **Namecheap** (namecheap.com) — cheapest, ~$10–15/year
- **Cloudflare** (cloudflare.com/products/registrar) — at-cost pricing, excellent DNS tools

Search for `flyingfishbook.com` (or `flyingfish.com`, `aflyingfish.com`, etc.).

---

### Step 2 — Add a CNAME file to the repo

Create a file called `CNAME` (no extension) in the root of this repo containing just the domain:

```
flyingfishbook.com
```

Commit and push it:

```bash
echo "flyingfishbook.com" > CNAME
git add CNAME
git commit -m "Add custom domain"
git push
```

---

### Step 3 — Point DNS to GitHub Pages

In your registrar's DNS settings, add these records:

**A records** (point the root domain to GitHub):

| Type | Host | Value |
|------|------|-------|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |

**CNAME record** (point www to GitHub):

| Type | Host | Value |
|------|------|-------|
| CNAME | www | tkunst.github.io |

DNS changes take anywhere from a few minutes to 48 hours to propagate (usually under an hour).

---

### Step 4 — Verify in GitHub settings

1. Go to https://github.com/tkunst/flying-fish-site/settings/pages
2. Under "Custom domain" you should see `flyingfishbook.com` (set automatically by the CNAME file)
3. Wait for the DNS check to pass (green checkmark)
4. Check "Enforce HTTPS" once it's available

---

## Adding Real Illustrations Later

When cover art or interior illustrations are ready:

1. Add image files to an `images/` folder in the repo
2. In `index.html`, replace the `.book-cover-placeholder` div with an `<img>` tag
3. In the hero, you can replace or supplement the CSS fish with a real illustration
4. Update the author avatar section with a real photo

---

## Contact for Site Issues

Site built: April 2026
Built with: Claude Code
