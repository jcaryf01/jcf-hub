# jcf-hub

Private personal hub served from **jcf-hub.jcfcllc.com** via GitHub Pages.
One repo → one subdomain → everything organized in folders.

## What's here

```
jcf-hub/
├── CNAME                     → jcf-hub.jcfcllc.com  (do not delete — binds the subdomain)
├── robots.txt                → blocks all search-engine indexing
├── index.html                → root "dead-end" page: a JCF monogram, NO links
├── assets/
│   └── hub.css               → shared navy-&-brass styles for all hub pages
├── hub-655b3b7228/           → the REAL navigation hub (unguessable path)
│   └── index.html            → links to Trips / Fish / Gym — this is what you bookmark
├── trips/
│   ├── index.html            → lists trips
│   ├── malaga.html           → served at /trips/malaga  (public itinerary, no tickets)
│   └── malaga-tickets.html   → served at /trips/malaga-tickets  (encrypted; passphrase-gated)
├── fish/
│   └── index.html            → placeholder
└── gym-routine/
    └── index.html            → placeholder
```

## How the privacy model works

- **The root** (`jcf-hub.jcfcllc.com`) shows only a monogram and the word "Private." No links, so anyone who discovers the hostname hits a dead end.
- **The real hub** lives at `jcf-hub.jcfcllc.com/hub-655b3b7228/` — an unguessable path, linked from nowhere. Bookmark it. That's your front door.
- Certificate Transparency logs expose the **hostname** (`jcf-hub.jcfcllc.com`) but never the **paths**, so `/hub-655b3b7228/`, `/trips`, `/fish` stay unlisted.
- `robots.txt` + a `noindex` tag on every page keep the whole subdomain out of Google.
- Obscurity is enough for personal odds-and-ends. For the one sensitive thing — **trip tickets** — don't rely on the path; use the **encrypted** file (`malaga-tickets.html`). It prompts for a passphrase only when opened.

## One-time deploy

1. Create a new GitHub repo (e.g. `jcf-hub`) and add these files (keep the folder layout).
2. Repo **Settings → Pages** → Source: *Deploy from a branch* → `main` / root.
3. In **Settings → Pages → Custom domain**, enter `jcf-hub.jcfcllc.com` → Save. (The `CNAME` file already contains this.)
4. In **Squarespace** (Settings → Domains → jcfcllc.com → DNS): add a **CNAME** record — Host `jcf-hub`, Value `YOURUSERNAME.github.io` (your account's Pages domain, no repo name). Leave the apex/www and MX records alone.
5. Wait for the DNS check to go green (up to ~24h, usually minutes), then tick **Enforce HTTPS**.
6. Recommended: **Settings → Pages → verify your domain** to prevent subdomain takeover.

Every `git push` after that auto-deploys.

## Add a new trip

1. Put `trip-name.html` in `/trips/` (and `trip-name-tickets.html` if it has an encrypted tickets copy).
2. Copy a row block in `/trips/index.html` and point it at `trip-name`.
3. Commit and push. Live in ~30 seconds at `jcf-hub.jcfcllc.com/trips/trip-name`.

## Add a new section (like the fish log)

1. Make a folder, e.g. `/fish/`, with an `index.html` (copy an existing section page).
2. Add a tile to `/hub-655b3b7228/index.html`.
3. Push.

## Notes

- File links are extension-less on GitHub Pages: `malaga.html` is reachable at `/trips/malaga`.
- Use lowercase, hyphens (not underscores or spaces) in file/folder names; paths are case-sensitive.
- If you ever want the hostname itself hidden from CT logs, put the domain behind Cloudflare (free) for a wildcard certificate — optional.
- To rotate the hub path, rename the `hub-655b3b7228/` folder to a new random string and re-bookmark. Nothing else references it except the section pages' "← Hub" links (update those too).
