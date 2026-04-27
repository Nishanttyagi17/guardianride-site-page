# guardianride.in — static landing page

A single-page marketing site, designed to be deployed on **GitHub Pages** at zero cost with a custom `.in` domain.

## What's in here

```
index.html         The landing page (single file: HTML + CSS + JS)
privacy.html       Placeholder privacy policy
terms.html         Placeholder terms of service
favicon.svg        Site icon
CNAME              Tells GitHub Pages your custom domain
.nojekyll          Tells Pages not to run Jekyll on these files
robots.txt         Search engine instructions
sitemap.xml        Search engine sitemap
```

## Cost

- GitHub Pages: **₹0/month** (free, with free SSL via Let's Encrypt)
- Domain (you already own `guardianride.in`): your existing renewal cost
- Formspree (for the contact form, optional): **₹0/month** for up to 50 submissions/month

Total recurring cost: **₹0/month** beyond your domain renewal.

---

## Step 1 — Customize the content

1. Open `index.html`. The brand name `GuardianRide` and contact email `guardianride1322@gmail.com` are already wired in. The only remaining placeholder is the form endpoint:
   - `https://formspree.io/f/YOUR_FORM_ID` → your real Formspree endpoint (see Step 4)
2. Update the hero stats and big counters (`500K+`, `50+`, `99.7%`, `4.9★`) with numbers that fit your business. Look for `data-counter="..."` attributes.
3. Edit the testimonials block to use real quotes once you have them — search for `class="testi"` in `index.html`.
4. Edit the partner names in the "Schools and operators we work with" strip (search for `class="partner"`).
5. Edit the FAQ content (search for `class="faq"`) to match the questions you actually get asked.
6. Update `privacy.html` and `terms.html` with your real legal text — get a lawyer to review before launch.

### Swapping in your own photos

The page uses three Unsplash photos (parent, driver, school feature sections) hotlinked from `images.unsplash.com`. Each has an automatic gradient fallback if the image fails to load.

To swap in your own photo, find the relevant `<img class="bg-photo" ...>` tag and replace the `src=` URL. You can:

- Upload your photos to the repo (e.g., `images/parent.jpg`) and reference them as `src="images/parent.jpg"`. This is the most reliable approach.
- Or pick different Unsplash photos — head to [unsplash.com](https://unsplash.com), pick a photo, right-click → "Copy image address", and paste in the `src=`.
- Or use a service like Pexels or your own CDN.

Recommended free, royalty-free photo sources: Unsplash, Pexels, Pixabay. Always check that the photo's license permits commercial use, and credit the photographer if requested.

> **Trademark heads-up:** "GuardianRide" is the brand name of the .com site. If you plan to use the same name for an independent business in the same industry, run it past a lawyer first to avoid a trademark dispute.

## Step 2 — Push to GitHub

```bash
# In this folder:
git init
git add .
git commit -m "Initial site"

# Create a new repository on github.com (e.g., named 'guardianride-site'). Then:
git branch -M main
git remote add origin https://github.com/YOUR-GITHUB-USERNAME/guardianride-site.git
git push -u origin main
```

## Step 3 — Enable GitHub Pages

1. On GitHub, go to your repo → **Settings → Pages**.
2. Under **Source**, choose **Deploy from a branch**.
3. Pick branch **main**, folder **/ (root)**. Save.
4. Within ~60 seconds, the site is live at `https://YOUR-GITHUB-USERNAME.github.io/guardianride-site/`.
5. In the same Pages settings, under **Custom domain**, enter `guardianride.in` and save. (The CNAME file in the repo also handles this.)

## Step 4 — Point your `.in` domain at GitHub Pages

In your domain registrar's DNS panel (where you bought `guardianride.in`), set up:

**For the apex domain `guardianride.in` — add four A records, all pointing to:**

```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**For `www.guardianride.in` — add a CNAME record:**

```
www  CNAME  YOUR-GITHUB-USERNAME.github.io
```

DNS can take a few minutes to a few hours to propagate. Once it does:

1. Go back to GitHub → Settings → Pages.
2. Wait for the "DNS check successful" green tick next to your domain.
3. Tick **Enforce HTTPS**. (You may need to wait ~10–30 min after DNS verification before this checkbox unlocks while GitHub provisions a Let's Encrypt cert.)

You're live at `https://guardianride.in`.

## Step 5 — Wire up the contact form (free)

The form posts to Formspree (free, no backend required):

1. Sign up at [formspree.io](https://formspree.io) (free plan = 50 submissions/month).
2. Create a new form. Copy your form endpoint, e.g., `https://formspree.io/f/abcd1234`.
3. In `index.html`, find `https://formspree.io/f/YOUR_FORM_ID` and replace with your endpoint.
4. Commit and push. Form submissions will arrive in your Formspree dashboard and your registered email.

If you outgrow Formspree, easy replacements: Web3Forms, Getform, Basin, or Cloudflare Workers.

---

## Why static (and not Rails)?

The marketing site has no dynamic behavior — no logged-in users, no payments, no inventory. Rails would require a paid host (Render, Railway, Fly.io — all $5+/month) and a database, for zero functional benefit on this page.

When you eventually need a backend (driver auth, parent app API, school dashboard data), build it as a **separate service** at `app.guardianride.in` or `api.guardianride.in`. That keeps the marketing page fast and free, and the app on the right tool for the job.

## Updating the site later

Edit any file, then:

```bash
git add .
git commit -m "Updated copy"
git push
```

GitHub Pages re-deploys automatically within seconds.
