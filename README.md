# prabudhd.me

Personal + academic site. Static HTML, no build step, no dependencies.

```
index.html      # the whole site (inline CSS + JS)
CNAME           # tells GitHub Pages the custom domain
.nojekyll       # skip Jekyll processing
robots.txt
sitemap.xml
assets/
  Prabudhd_Kandpal_Resume.pdf
```

## Deploy to GitHub Pages

You already have `prabudhd2003/prabudhd2003.github.io`, which is a **user site** —
it serves at the repo root, so this is the easiest home for it.

```bash
git clone https://github.com/prabudhd2003/prabudhd2003.github.io.git
cd prabudhd2003.github.io

# copy everything from this folder in (including the dotfile)
cp -R /path/to/site/. .

git add -A
git commit -m "New personal site"
git push origin main    # or master, whichever the repo uses
```

Then in the repo: **Settings → Pages**
- Source: *Deploy from a branch*, branch `main`, folder `/ (root)`
- Custom domain: `prabudhd.me` → Save
- Tick **Enforce HTTPS** once the certificate is issued (can take up to ~1 hour)

## DNS for prabudhd.me

At your registrar, delete any existing A/AAAA/CNAME records for the apex and `www`, then add:

**Apex (`@` / blank host) — four A records:**

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**And the four AAAA records (IPv6, optional but recommended):**

```
2606:50c0:8000::153
2606:50c0:8001::153
2606:50c0:8002::153
2606:50c0:8003::153
```

**`www` — one CNAME:**

```
www  →  prabudhd2003.github.io
```

DNS usually propagates in 10–60 minutes. Verify with:

```bash
dig prabudhd.me +short
```

> These are GitHub's published Pages IPs. If it's been more than a year since this was
> written, confirm them at
> <https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site>.

## Editing

Everything lives in `index.html`. The sections are commented (`<!-- ==== PROJECTS ==== -->`).

**Add a project:** copy a `<a class="card">` block inside `#grid`. The `data-t`
attribute holds space-separated filter tags — they must match a `data-f` value on one
of the filter buttons (`ml`, `llm`, `rl`, `systems`, `web`). Add `class="card star"`
for the amber border, and a `<span class="badge">` for the corner label.

**Change colors:** the `:root` block at the top of the `<style>` tag. `--accent` is the
amber; `--bg`, `--surface`, `--ink*` are background and text. The `html[data-theme="light"]`
block right below it is the light palette.

## TODO for you

- [ ] Add your Google Scholar URL — search `ORCID` in `index.html`, there's a spot next to it
- [ ] Swap in a real headshot if you want one (the layout has room in the About sidebar)
- [ ] Update the résumé PDF in `assets/` whenever you revise it
