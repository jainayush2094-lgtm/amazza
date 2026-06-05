# Amazza — website (Phase 1 build)

A static, self-hosted site for GitHub Pages, with a Sveltia CMS backend so products and
text can be edited through a form at `/admin` — no code.

The site works **right now** with sample content (elegant tonal placeholders stand in for
photos). Add real assets later and they replace the placeholders automatically.

---

## Folder structure

```
amazza-site/
├─ index.html            ← the homepage (reads its content from /data)
├─ 404.html              ← branded "page not found"
├─ robots.txt            ← search-engine rules
├─ sitemap.xml           ← for Google Search Console
├─ data/                 ← THE EDITABLE CONTENT (the CMS writes here)
│  ├─ site.json          ← hero text, philosophy, craft text, email, WhatsApp, hero film
│  ├─ products.json      ← the six collections
│  └─ spaces.json        ← the three lookbook scenes
├─ admin/                ← the editing backend
│  ├─ index.html         ← loads Sveltia CMS
│  └─ config.yml         ← defines what's editable (CHANGE the 2 placeholders, see below)
├─ images/
│  ├─ hero/              ← hero still / poster      (16:9, ~2400×1350, <500KB)
│  ├─ collections/       ← the six collection shots (1:1 square, ~1600×1600, <300KB each)
│  ├─ spaces/            ← lookbook scenes          (1 portrait 3:4, 2 landscape 4:3, <400KB)
│  ├─ craft/             ← brass/finish macro       (1:1 square, ~1600×1600)
│  ├─ brand/             ← logo (svg), favicon.svg, og-image.jpg (1200×630)
│  └─ uploads/           ← photos added through /admin land here automatically
└─ video/                ← hero film: hero.mp4 (1080p, MP4/H.264, 10–15s, 2–4MB)
```

---

## Two things to change in `admin/config.yml` before the CMS works

1. `repo:` → your repo, e.g. `jainayush2094-lgtm/amazza`
2. `base_url:` → your Cloudflare `sveltia-cms-auth` worker URL (set up in Phase 5)

---

## How to swap in real content

**Easiest — through the CMS:** go to `your-domain/admin`, log in with GitHub, edit the
fields, upload photos, Save. Done.

**By hand (optional):** drop a photo into the right `images/…` folder, then put its path
into the matching field in the `data/*.json` file, e.g.
`"image": "images/collections/colore.jpg"`. If `image` is left blank, the tonal
placeholder shows instead — so nothing ever looks broken.

---

## The hero film (top of the homepage)

- Format: **MP4 (H.264)**, muted, autoplay, loops. Length **10–15s**. Size **2–4MB** (max ~5MB).
- Resolution 1080p (1920×1080). Quiet motion only — water, light, a slow drift.
- Put the file at `video/hero.mp4`, set `heroVideo` to `video/hero.mp4` in `site.json`
  (or via the CMS), and add a `heroPoster` still as the fallback.
- Leave `heroVideo` blank to keep the cinematic animated still (recommended to launch with).

---

## Going live

Follow the phase guide: create the GitHub repo → enable Pages → connect the domain
(A records 185.199.108–111.153, `www` CNAME) → Zoho email → deploy the CMS auth worker.

GitHub Pages apex A records:
`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`

---

## Note on previewing locally

`index.html` fetches the `/data` files over HTTP. Opening the file directly from disk
(double-click) may block that fetch — in which case it falls back to built-in sample
content and still renders. Served over GitHub Pages (or any web server) it reads the
real data files.
