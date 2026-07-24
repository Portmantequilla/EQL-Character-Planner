# Deploying beecanyonretro.com (GitHub Pages)

This folder is the complete website — one self-contained `index.html` (all art and fonts
inlined), the download zips, and the source assets. No build step, no dependencies.

## One-time setup (~10 minutes)

### 1. Create the GitHub repository

1. Sign in (or sign up) at github.com — this same account can later host the
   EQL Character Builder app repo.
2. Create a new **public** repository, e.g. `beecanyon-site`. Don't add a README.

### 2. Push this folder

From a terminal in this folder (`E:\EQLBuilder\website`):

```
git init
git add .
git commit -m "Bee Canyon Gaming — EQL Character Builder site v1"
git branch -M main
git remote add origin https://github.com/<YOUR-USER>/beecanyon-site.git
git push -u origin main
```

(Or use GitHub Desktop / the web "upload files" page — drag the folder contents in.)

### 3. Turn on GitHub Pages

Repo → **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → Save.
After a minute the site is live at `https://<YOUR-USER>.github.io/beecanyon-site/`.

### 4. Point the domain (in Wix)

The domain is registered at Wix; you're only changing its DNS records — the Wix site and
Premium plan are untouched.

Wix Dashboard → **Domains** → beecanyonretro.com → **Manage DNS records**:

- **A records** for the bare domain (`beecanyonretro.com`) — replace the existing A record(s) with these four:
  - `185.199.108.153`
  - `185.199.109.153`
  - `185.199.110.153`
  - `185.199.111.153`
- **CNAME** for `www` → `<YOUR-USER>.github.io`

### 5. Tell Pages about the domain

Repo → Settings → Pages → **Custom domain** → enter `www.beecanyonretro.com` → Save
(the `CNAME` file in this folder already matches). Tick **Enforce HTTPS** once the
certificate is issued (can take up to an hour after DNS propagates).

DNS propagation is usually minutes, occasionally a few hours. The old Wix site keeps
working at its wixsite.com address the whole time, and flipping the DNS back reverts
everything — this change is fully reversible.

## Updating the site later

Edit `index.html` (or ask Claude to regenerate it from the design source at
`E:\EQLBuilder\site\redesign-2026-07\`), commit, push. Pages redeploys automatically.

New app releases: drop the new zips into `downloads/`, update the version text, sizes and
SHA-256 hashes in `index.html`, push.

## What's in here

- `index.html` — the whole site, self-contained (Cinzel font + all images inlined as data URIs)
- `downloads/` — the v0.2.0 release zips the download buttons link to
- `assets/` — the individual optimized images + the intro GIF (referenced by the page and
  kept separately for future editing)
- `CNAME` — tells GitHub Pages the custom domain
