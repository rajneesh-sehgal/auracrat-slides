# AURAcrat Slides

Presentation hosting for Raj Sehgal — The AI Guy.

A lightweight static site served by Nginx. Add an HTML file, update `index.html`, push to GitHub. Coolify redeploys in under a minute.

---

## Repo Structure

```
auracrat-slides/
├── index.html                          ← Home page (update when adding a presentation)
├── presentations/
│   └── ai-fundamentals-raj-sehgal.html
├── nginx.conf                          ← Nginx server config
├── Dockerfile                          ← Coolify picks this up automatically
└── README.md
```

---

## Adding a New Presentation

1. Drop the HTML file into `/presentations/`
2. Add a new card to `index.html` — copy the existing card block and update:
   - `href` pointing to the new file
   - Title, subtitle, audience, duration, venue, slide count
   - Date in the meta row
   - Tag colour if needed (use `green` class for a different accent)
3. Push to GitHub — Coolify deploys automatically

---

## Local Testing

```bash
# Option 1: Python (no install needed)
cd auracrat-slides
python3 -m http.server 8080
# Open http://localhost:8080

# Option 2: Docker
docker build -t auracrat-slides .
docker run -p 8080:80 auracrat-slides
# Open http://localhost:8080
```

---

## Coolify Setup (first time)

1. In Coolify, go to **Resources → Add New Resource → Docker**
2. Connect your GitHub repo
3. Set **Branch** to `main`
4. Coolify will detect the `Dockerfile` automatically
5. Set **Port** to `80`
6. Under **Domains**, add `slides.auracrat.com` (or your preferred subdomain)
7. Enable **Automatic Deploy on Push** — every GitHub push triggers a redeploy
8. Click **Deploy**

Total setup time: under 10 minutes.

---

## Updating a Presentation

Replace the HTML file in `/presentations/` and push. No other changes needed.
The nginx cache header for HTML files is set to `no-cache` so visitors always get the latest version immediately.

---

## Custom Domain DNS

Point `slides.auracrat.com` to your VPS IP with an A record.
Coolify handles SSL via Let's Encrypt automatically once the domain resolves.

```
Type  Name    Value
A     slides  YOUR_VPS_IP
```
