# Tegmaro — static site

Two-page static site (landing + sneak peek) served by Caddy, packaged for Railway.

```
tegmaro/
├── Dockerfile        # caddy:2-alpine, copies site/ to /srv
├── Caddyfile         # binds to $PORT, gzip, clean URLs
└── site/
    ├── index.html
    ├── sneak-peek.html
    ├── blueprint-visual.png
    ├── hero-visual.png
    └── mission-visual.png
```

## Deploy to Railway

**Option A — CLI (fastest, no repo needed):**

```bash
cd tegmaro
railway init          # create a new project (or `railway link` to an existing one)
railway up            # builds the Dockerfile and deploys
railway domain        # generate a public *.up.railway.app domain
```

**Option B — GitHub:**

Push this folder to a repo, then in Railway: New Project → Deploy from GitHub repo. Railway auto-detects the Dockerfile. Generate a domain under Settings → Networking.

## Notes

- Caddy listens on Railway's injected `PORT` (falls back to 8080 locally).
- `/sneak-peek` resolves without the `.html` extension via `try_files`.
- To point `tegmaro.com` at it later: add the custom domain in Railway → Settings → Networking, then create the CNAME it gives you at your registrar.

## Local preview

```bash
docker build -t tegmaro . && docker run -p 8080:8080 tegmaro
# → http://localhost:8080
```
