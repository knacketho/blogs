# Knacketho Blogs — How to Add a New Article

## Current Structure

```
main.html
art1/
  index.html                              ← Article: Building Your In-House CloudOps Team
  files/
    ansible-cert-deploy-sample.txt
    azure-cert-management-architecture.txt
art2/
  index.html                              ← Article: Taming GCP AI Cost Spikes (FinOps White Paper)
  files/
    GCP_AI_Cost_Governance_WhitePaper.pdf
README.md
```

---

## Adding Article 3 (art3)

### Step 1 — Create the folder

```
art3/
  index.html
  files/        ← drop any PDFs, TXTs, or other downloads here
```

### Step 2 — Build the article page (art3/index.html)

Two options depending on the type of article:

**Option A — Standard written article**
Copy `art1/index.html` as your starting template.
- Update the `<title>` tag
- Update the `.meta` tags (tags, date, read time)
- Update `<h1>` with your article title
- Update the `.lede` paragraph (intro summary)
- Replace all content inside `.body`
- Update the Downloads section — add your files or remove the block if no downloads
- All links back to main use `../main.html` (already correct if copied from art1)

**Option B — Visual / landing-style article (like art2)**
Use your own custom HTML design.
- Make sure the nav logo links to `../main.html`
- Add an `← All articles` link in the nav and footer pointing to `../main.html`
- Any downloadable files should go in `art3/files/` and be referenced as `files/filename.pdf`

### Step 3 — Add the downloads (optional)

Drop files into `art3/files/`.

In `art3/index.html`, inside the `.downloads` block, copy one `<li>` entry and update:
- `href="files/your-filename.pdf"` 
- `.file-name` — the filename shown to the user
- `.file-desc` — one-line description
- `.file-dl` badge — change extension label (`.pdf`, `.txt`, etc.)

Update the `downloads-subtitle` count (e.g. `1 file`, `2 files`).

### Step 4 — Add the card to main.html

Open `main.html` and find the comment:

```html
<!-- ARTICLE 2 -->
```

**Paste a new card block ABOVE it** (newest article always at the top). Copy the art2 `<li>` block and update:

```html
<li>
  <a class="card" href="art3/index.html"
     data-search="your keywords here for search">
    <span class="card-num">03</span>
    <div class="card-body">
      <div class="card-title">Your Article Title</div>
      <div class="card-excerpt">
        One or two sentence summary shown on the main page.
      </div>
      <div class="card-foot">
        <span class="tag">Tag1</span>
        <span class="tag">Tag2</span>
        <span class="dot">·</span>
        <span class="card-date">Month YYYY</span>
        <span class="dot">·</span>
        <span class="card-read">X min</span>
        <span class="file-badge">           ← remove this block if no downloads
          <svg ...></svg>
          1 file
        </span>
      </div>
    </div>
    <svg class="card-arrow" ...>...</svg>
  </a>
</li>
```

### Step 5 — Update the article count

In `main.html`, find this line near the top of the articles section:

```html
<span class="count" id="count">2 articles</span>
```

Change it to:

```html
<span class="count" id="count">3 articles</span>
```

---

## Search

The search bar on `main.html` filters on the `data-search` attribute of each card.
Put all relevant keywords there — title words, tags, topic terms — in lowercase.

Example:
```html
data-search="gcp finops vertex ai gemini cost governance cloud billing"
```

---

## Quick Checklist

- [ ] Created `art3/` folder
- [ ] Created `art3/index.html` (from template or custom)
- [ ] Nav logo links to `../main.html`
- [ ] Back link (`← All articles`) in nav and footer → `../main.html`
- [ ] Files dropped into `art3/files/`
- [ ] Download hrefs use `files/filename.ext`
- [ ] New `<li>` card added at the TOP of the list in `main.html`
- [ ] `data-search` filled with relevant keywords
- [ ] Article count updated in `main.html` (2 → 3)
- [ ] Tested locally: open `main.html`, click card, verify download works

---

## Local Testing

Because download links are relative paths, open via a local server rather than double-clicking the HTML file:

```bash
cd /path/to/site
python3 -m http.server 8080
# then open http://localhost:8080/main.html
```

## Hosting (GitHub Pages)

Push the entire folder to your GitHub repo root.
Go to **Settings → Pages → Source: main branch / root**.
Site will be live at `https://yourusername.github.io` or your custom domain.
