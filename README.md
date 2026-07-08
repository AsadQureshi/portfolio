# Asad Ali Qureshi — Portfolio

A single-page portfolio site for Asad Ali Qureshi, Senior Full-Stack Developer & Team Lead.
Static HTML/CSS/JS — no framework, no build step, no dependencies to install.

**Live sections:** Hero · About · Stack · Projects · Experience · Side Venture · FAQ · Client Feedback · Contact

---

## 1. Project structure

```
portfolio/
├── index.html      ← the entire site (HTML + CSS + JS in one file)
├── README.md        ← this file
└── assets/
    ├── profile-photo.jpg              (kept for reference — already embedded in index.html)
    ├── Asad-Ali-Qureshi-CV.pdf        (kept for reference — already embedded in index.html)
    ├── exploretech-screenshot.jpg     (kept for reference — already embedded in index.html)
    └── rakam-screenshot.jpg           (kept for reference — already embedded in index.html)
```

**Important:** the profile photo, CV, and project screenshots are embedded directly inside
`index.html` as base64 data — this was done deliberately so the site works as a single
portable file with no broken links, regardless of how or where it's opened or hosted.
The copies in `assets/` are kept only as originals for future edits (see section 4).

---

## 2. Deploy to Vercel (free)

You only strictly need `index.html` to deploy — it's fully self-contained.

### Option A — GitHub → Vercel (recommended, easiest to keep updating)

1. **Push to GitHub** (skip if already done):
   ```bash
   cd portfolio
   git init
   git add .
   git commit -m "Initial portfolio site"
   git branch -M main
   ```
   Create a new repo at [github.com/new](https://github.com/new) (don't initialize it with a README),
   then:
   ```bash
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
   git push -u origin main
   ```

2. **Import into Vercel:**
   - Go to [vercel.com](https://vercel.com) → sign up / log in (GitHub login is easiest)
   - Click **Add New → Project → Import Git Repository**
   - Select your repo
   - Framework preset: **Other** (no build command needed — it's plain HTML)
   - Click **Deploy**

3. You'll get a live URL like `your-project.vercel.app` in under a minute. Every future
   `git push` to `main` will auto-redeploy the site.

### Option B — Drag-and-drop (no GitHub needed)

1. Go to [vercel.com](https://vercel.com) → sign up / log in
2. **Add New → Project**
3. Drag the `portfolio` folder onto the upload area
4. Framework preset: **Other**
5. Click **Deploy**

### Option C — Vercel CLI

```bash
npm install -g vercel
cd portfolio
vercel          # deploys a preview
vercel --prod   # pushes to your production URL
```

### Custom domain

Once deployed: Vercel dashboard → your project → **Settings → Domains** → add your domain
and follow the DNS instructions shown there.

---

## 3. Public vs. private repo

Either is fine. A few things worth knowing before making it public:

- The CV (embedded in `index.html`) contains personal details (phone, DOB, etc.) — anyone
  with the repo link can extract and view it. That's normal for a portfolio aimed at
  recruiters, but double-check there's nothing on it you wouldn't want fully public.
- No API keys, secrets, or credentials exist anywhere in this project — safe either way on that front.

---

## 4. Editing content later

Everything lives in `index.html`, organized by clearly commented sections
(`<!-- HERO -->`, `<!-- ABOUT -->`, `<!-- PROJECTS -->`, etc.) — search for the comment to
jump straight to a section.

### Text content
Just edit the text directly inside the relevant `<section>` tag.

### Replacing the photo, CV, or project screenshots
These are embedded as base64 so they can't be swapped by simply replacing a file. To update one:

1. Put your new file in `assets/` (e.g. `assets/profile-photo.jpg`)
2. Convert it to base64 and re-embed it. If you have Python available:
   ```python
   import base64
   with open('assets/profile-photo.jpg', 'rb') as f:
       b64 = base64.b64encode(f.read()).decode('utf-8')
   print(f'data:image/jpeg;base64,{b64}')
   ```
   Paste the printed string in as the new `src` (for images) or `href` (for the CV PDF,
   use `data:application/pdf;base64,...`) inside `index.html`.
3. Or — simplest option — drop the file back into a chat with Claude and ask it to
   re-embed the update for you.

### Adding a new project card
Copy one `.project-card` block inside the `<!-- PROJECTS -->` section, update the image,
heading, description, and tag list.

### Adding/editing FAQ items
Copy one `.faq-item` block inside the `<!-- FAQ -->` section and edit the question/answer text.

### Updating testimonials
The `<!-- TESTIMONIALS -->` section currently has **3 placeholder cards** — replace the
placeholder quote and `Client Name` / `Role · Company` text with real client feedback
before publishing live. Star rating is plain text (`★★★★★`) — trim stars for a lower rating
if needed.

---

## 5. Design system reference

| Token | Value | Use |
|---|---|---|
| `--bg` | `#0F1419` | Page background |
| `--bg-alt` | `#141B22` | Section/card background |
| `--text` | `#E7E2D6` | Primary text |
| `--text-dim` | `#8B95A1` | Secondary text |
| `--accent` | `#C98A3E` | Copper accent (links, highlights) |
| `--accent-2` | `#5B7C99` | Slate blue secondary accent |

Fonts: **Fraunces** (headings/serif), **Inter** (body), **JetBrains Mono** (labels/code-style text) — loaded via Google Fonts CDN in the `<head>`.

---

## 6. Browser support

Plain HTML/CSS/JS, no build step — works in all modern browsers. Uses `IntersectionObserver`
for scroll-reveal animations (supported everywhere except very old browsers) and respects
`prefers-reduced-motion`.
