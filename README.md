# A Fish! A Fish! A Flying Fish!

Website for the picture book *A Fish! A Fish! A Flying Fish!* by Trisha Kunst.

## Hosting

Hosted via GitHub Pages. To deploy:
1. Push to the `main` branch
2. Go to repo Settings → Pages → Source: Deploy from branch → `main` / `/ (root)`
3. Site will be live at `https://tkunst.github.io/flying-fish-site/`

## Adding a Custom Domain

1. Buy a domain (e.g., `flyingfishbook.com`) at Namecheap or Cloudflare
2. Add a `CNAME` file to this repo containing just the domain name
3. Point the domain's DNS to GitHub Pages IPs (see GitHub Pages docs)

## Updating Content

- `index.html` — all page content
- `css/style.css` — all styles and colors
- Replace the `TK` initials avatar with a real author photo when available
- Replace the CSS fish cover placeholder with real cover art when available

## Privacy pre-push hook (fresh clones — read this if a push is blocked)

This is a **public** repository. It ships a local `pre-push` git hook that scans
what you are about to push and **blocks the push** if it finds configured private
strings (names, etc.) in tracked text or in a PDF's text layer — so they cannot be
published by mistake. It is a local prevention layer only; there is no CI for it.

Enable it after cloning:

```sh
scripts/install-hooks.sh
```

That sets `core.hooksPath=.githooks` for this clone.

### Fail-closed behavior (this will bite a fresh clone)

The hook is **fail-closed and global to every clone**. Once `install-hooks.sh` has
run on a machine, that machine **cannot push this repo** (or any other repo that
uses this hook) until a local term-list file exists at:

```text
~/.config/privacy-gate/terms.txt
```

The term list is **deliberately not stored in this repository** — committing the
private strings would publish exactly what the hook is meant to protect. A fresh
clone that lacks the file will therefore see **every push blocked**, with:

```text
privacy_scan: no terms configured.
Create ~/.config/privacy-gate/terms.txt (one term per line).
Push blocked by privacy gate.
```

Fix it by creating the file (one private string per line; blank lines and lines
starting with `#` are ignored):

```sh
mkdir -p ~/.config/privacy-gate
"$EDITOR" ~/.config/privacy-gate/terms.txt
```

Then push again.

### Other behavior and troubleshooting

- **Matching** is case-insensitive and fixed-string. Committed data files
  (`*.csv`, `*.xlsx`, `*.xls`) are skipped by the text scan, because public
  datasets contain unrelated real names by design.
- **Non-searchable (image-only) PDFs are blocked**, because their text cannot be
  read. Make the PDF searchable first — `ocrmypdf in.pdf out.pdf`, or `vision-ocr`
  for higher accuracy on hard scans — then re-check. Searchable PDFs have their
  text layer scanned like any other text.
- **Emergency bypass:** `git push --no-verify` skips the hook. Use it only when you
  are certain the content is clean.
- **Disable the hook entirely:** `git config --unset core.hooksPath`.
