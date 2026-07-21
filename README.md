# Personal site — plain HTML, hosted free on GitHub Pages

No build step, no framework, no database. Every page is a real `.html` file
you can open and edit directly. Publishing a change is just: edit → commit → push.

## Structure

```
.
├── index.html                     # homepage — intro + experience (left), portrait (right)
├── essays.html                     # list of all short essays, with intro blurbs
├── research.html                    # list of research projects (PDF + code links)
├── data.html                         # full table of datasets + source links
├── contact.html                       # email + thank-you page
├── style.css                           # all styling, shared across every page
├── essays/
│   └── example-essay.html             # copy this file to add a new essay
├── papers/
│   └── eaf-transition-china.html      # one page per paper, links to PDF + GitHub code
└── assets/
    ├── portrait.jpg                    # your photo goes here (see below)
    └── pdfs/
        └── eaf-transition-china.pdf    # the actual paper files live here
```

## Layout

- A vertical nav rail runs down the far left of every page: **Index, Short
  Essays, Research Projects, Data, Contact**. On narrow screens it collapses
  into a horizontal bar at the top.
- The homepage (`index.html`) splits into two columns: your intro + experience
  on the left, your portrait on the right (`.home-split` in `style.css`).
- `essays.html` and `research.html` are listing pages — each entry has a
  title, a short blurb, and links out to the full piece.

## Adding your photo

Save a portrait as `assets/portrait.jpg` (roughly 4:5 ratio, e.g. 800×1000px
works well), then in `index.html` replace:

```html
<div class="placeholder">Add your photo:<br>assets/portrait.jpg<br>(≈4:5 ratio, e.g. 800×1000px)</div>
```

with:

```html
<img src="assets/portrait.jpg" alt="Your Name">
```

## How to add a new essay

1. Copy `essays/example-essay.html` to a new file, e.g. `essays/my-new-essay.html`.
2. Edit the `<title>`, the `<p class="eyebrow">` date, the `<h1>`, and the body
   paragraphs.
3. Add a new `<li class="entry">` block to `essays.html`, pointing at your
   new file. Copy an existing `<li>` and change the tag, title, link, and blurb.
4. Commit and push.

## How to add a new research paper (and its code)

1. Drop the PDF into `assets/pdfs/`, e.g. `assets/pdfs/my-second-paper.pdf`.
2. Copy `papers/eaf-transition-china.html` to `papers/my-second-paper.html`.
   Update the title, abstract, and both links in the `.pdf-card` block (PDF
   + code repo).
3. Add a new `<li class="entry">` to `research.html` with a **PDF** and
   **Code** link.
4. Commit and push.

### Where should the code live?

Keep source code in its own GitHub repo per paper (e.g.
`github.com/yourname/eaf-transition-china`), rather than embedding it in the
site. Reasons:

- It gets its own README, commit history, issues, and license — useful if
  someone wants to replicate your work or you want to point a search
  committee at clean, documented code.
- It keeps the website itself simple and fast — this site just links out to
  the repo, it doesn't need to render or host the code.
- If a paper used data under NDA (like your SMM data), the repo's README is
  a natural place to note that and point to the public equivalent instead —
  keeping that caveat out of the main site.

If you'd rather keep everything in one place, a single `research-code`
monorepo with one subfolder per paper works too — just link to the subfolder
path from each paper's page.

## How to add a new dataset

Open `data.html` and add one `<tr>` row to the table with the dataset name,
its source link, and a short note (e.g. if it's a public equivalent for a
proprietary source under NDA).

## How to update contact info

Edit `contact.html` — the email link is a single `mailto:` line near the
bottom of the file.

## Hosting on GitHub Pages (free)

1. Create a new GitHub repo, e.g. `yourname.github.io` (using your GitHub
   username gives you a clean root-level URL) — or any repo name if you're
   fine with a `/reponame/` path.
2. Push all these files to the repo's `main` branch.
3. In the repo settings → **Pages**, set source to `Deploy from a branch`,
   branch `main`, folder `/ (root)`.
4. Your site goes live at `https://yourusername.github.io` (or
   `https://yourusername.github.io/reponame`) within a minute or two.
5. Every future `git push` redeploys automatically — no other steps.

## Design notes

- Fonts: **Fraunces** (display/headings), **Inter** (body), **IBM Plex Mono**
  (dates, tags, nav labels) — loaded from Google Fonts via `<link>` tags in
  each page's `<head>`.
- Colors and spacing are CSS variables at the top of `style.css`
  (`:root { ... }`) — change them once and every page updates.
- The nav rail's current-page indicator is a small oxide-orange bar (`.current::before`
  in `style.css`) — make sure each page's copy of the nav has `class="current"`
  on the right link.
- Everything is responsive down to mobile and works with keyboard navigation.

## Local preview

No server needed — just open `index.html` in a browser. If you want relative
links to behave exactly like they will on GitHub Pages, you can instead run
a tiny local server from this folder:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000`.
