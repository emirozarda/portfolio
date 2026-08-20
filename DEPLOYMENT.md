# Deployment Guide

## 1. Hosting recommendation: Cloudflare Pages

| | Cloudflare Pages | GitHub Pages | Netlify | Vercel |
|---|---|---|---|---|
| Cost | Free | Free | Free | Free |
| Bandwidth | Unlimited | ~100 GB/mo soft limit | 100 GB/mo | 100 GB/mo |
| Custom domain | Free, easy | Free | Free | Free |
| SSL | Automatic | Automatic | Automatic | Automatic |
| Build minutes (not needed here) | 500/mo | N/A | 300/mo | 100 GB-hrs |
| Global CDN | Yes (very large network) | Yes | Yes | Yes |
| Git-based auto-deploy | Yes | Yes | Yes | Yes |
| Video file hosting | Fine at this size | Fine | Fine | Fine |

**Recommendation: Cloudflare Pages.** For a static site like this, all four options
would work well, but Cloudflare Pages wins on three points that matter for you
specifically:

1. **Unlimited bandwidth** — the others cap free-tier bandwidth; Cloudflare doesn't,
   so a portfolio getting shared with several recruiters or going semi-viral on
   LinkedIn never risks a surprise limit.
2. **Fastest global edge network** — Cloudflare's CDN has more points of presence
   than the alternatives, so load times are consistently fast worldwide.
3. **Cloudflare also does domains** — if you buy a domain later, Cloudflare sells
   them at wholesale price (no markup), and having the domain and host in the same
   account makes DNS setup a two-click process instead of manually pointing
   nameservers between two providers.

GitHub Pages is a fine second choice if you'd rather keep everything inside GitHub's
own ecosystem, but Cloudflare Pages still deploys directly from a GitHub repo, so
you get GitHub's version history either way.

---

## 2. What you need: GitHub + Cloudflare accounts

You'll push your site's code to a GitHub repository, then tell Cloudflare Pages to
watch that repository and redeploy automatically every time you push a change.

1. Create a free GitHub account at [github.com](https://github.com) if you don't
   have one.
2. Create a free Cloudflare account at [dash.cloudflare.com/sign-up](https://dash.cloudflare.com/sign-up).

---

## 3. Push the site to GitHub

If you're comfortable with the command line:

```bash
cd path/to/this/folder
git init
git add .
git commit -m "Initial portfolio site"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/portfolio.git
git push -u origin main
```

(Create the empty `portfolio` repository on GitHub first — go to
[github.com/new](https://github.com/new), name it `portfolio` or anything you like,
leave it empty, no README/license, and copy the URL it gives you into the command
above.)

**If you'd rather avoid the command line:** go to your new GitHub repo page, click
"Add file → Upload files," and drag the entire site folder in. GitHub's web
uploader accepts folders and preserves the structure. This works fine for a site
this size.

---

## 4. Connect Cloudflare Pages to the repo

1. In the Cloudflare dashboard, go to **Workers & Pages → Create → Pages → Connect to Git**.
2. Authorize Cloudflare to access your GitHub account and select the `portfolio` repo.
3. Build settings:
   - **Framework preset:** None
   - **Build command:** *(leave blank)*
   - **Build output directory:** `/` (the root — this is a static site, nothing to build)
4. Click **Save and Deploy**.

Cloudflare will deploy the site and give you a free URL immediately, in the form:

```
https://portfolio-xyz.pages.dev
```

That URL is live, has SSL, and is on the free tier permanently — you can use it as
your portfolio link right away and add a custom domain whenever you're ready.

---

## 5. Adding a custom domain (later, when you're ready)

You told me you'll hold off on a domain for now — here's what to do when you're
ready, so you have it for reference.

**Buying a domain:**
- A `.com` domain typically runs **$10–15 CAD/year**. Cloudflare Registrar sells
  domains at cost (no markup) — usually the cheapest option once you're already
  hosting there. Namecheap and Google Domains (now also via Squarespace, ironically)
  are reasonable alternatives.
- Something like `emirozarda.com` or `emirozarda.ca` would both work well.

**Connecting it to Cloudflare Pages:**
1. If you bought the domain through Cloudflare Registrar, it's already on
   Cloudflare's nameservers — skip to step 3.
2. If you bought it elsewhere, go to **Websites → Add a site** in Cloudflare, enter
   your domain, and Cloudflare will give you two nameservers to set at your
   registrar (in their DNS settings). This can take a few hours to propagate.
3. In your Pages project, go to **Custom domains → Set up a custom domain**, enter
   your domain, and Cloudflare configures the DNS and SSL certificate automatically.

**About your old Squarespace domain:** if you don't already own the domain your
Squarespace site uses, you generally can't transfer it away from Squarespace — it's
tied to their account. If you want to keep using that exact domain name, you'd need
to check in your Squarespace domain settings whether you actually purchased and own
it (vs. Squarespace hosting it under a default subdomain). If you do own it, most
registrars support transferring a domain elsewhere; if you don't, you'd register it
fresh wherever it's available, or simply pick a new domain — the `.pages.dev` URL
works perfectly well in the meantime either way.

---

## 6. Making updates after deployment

Because Cloudflare Pages watches your GitHub repo, **every update follows the same
pattern**: change a file, push it, and the live site updates automatically within
about a minute. No redeploying by hand.

### Editing text
Open the relevant `.html` file in any text editor (VS Code is a good free option),
find the text, change it, save.

### Adding a new project
1. Duplicate `projects/smart-carrier.html` (the simplest project page) as a
   starting template.
2. Rename it, e.g. `projects/my-new-project.html`.
3. Edit the title, description, stats, and body content.
4. Add a new card for it in `projects/index.html` (copy one of the existing
   `<a class="project-card">` blocks) and, if you want it on the homepage too, in
   `index.html`.

### Replacing or adding images
1. Drop the image file into `images/quadcopter/`, `images/cnc/`, or a new folder
   you create under `images/`.
2. Reference it in the HTML with `<img src="/images/your-folder/filename.jpg" alt="...">`.
3. Keep images under ~200KB where possible for fast load times — you can resize
   and compress with any free tool (Squoosh.app is a good browser-based one) before
   uploading.

### Updating your resume
Replace `resume.pdf` with your new file, keeping the exact filename `resume.pdf`,
and it updates everywhere it's linked (the Resume page and its download button).

### Pushing an update via GitHub's web interface (no command line needed)
1. Go to the file in your GitHub repo.
2. Click the pencil (edit) icon, or "Upload files" to replace an image/PDF.
3. Make your change, scroll down, click **Commit changes**.
4. Cloudflare Pages redeploys automatically — check the **Workers & Pages** tab in
   Cloudflare for deploy status, usually done in under a minute.

---

## 7. Final QA checklist (already reviewed, listed here for your own future passes)

- [x] Desktop responsiveness — checked at 1440px
- [x] Mobile responsiveness — checked at 390px
- [x] All internal links resolve (automated check passed)
- [x] All images load and have descriptive alt text
- [x] Resume download button works, links to `/resume.pdf`
- [x] LinkedIn link → `linkedin.com/in/emir-ozarda-8288ab197`
- [x] GrabCAD link → `grabcad.com/emir.ozarda-2`
- [x] Email link → `mailto:emirozarda@hotmail.com`
- [x] No content invented beyond your resume and existing site
- [x] SEO: titles, meta descriptions, OG tags, sitemap.xml, robots.txt all present
- [ ] Proofread every page's copy yourself once more before sharing the link — I
      wrote the case-study language, so it's worth a pass in your own voice
- [ ] Add photos for the Smart Carrier project once you have them (currently
      text-only, at your request)
