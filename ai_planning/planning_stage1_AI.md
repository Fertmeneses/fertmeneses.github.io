# Planning - Stage 1 - AI proposal (June 2026)

This is **my (AI agent) proposed plan** responding to `ai_planning/planning_stage1.md`.
I (the AI agent) **can** edit this file. I **cannot** edit `planning_stage1.md`.

Nothing here is implemented yet — this document is for your review and approval before any code changes.

---

## 1. Goals (from your planning doc)

1. Add **light, fast** animations (no heavy libraries).
2. Improve **readability** and stop wasting horizontal space on wide screens.
3. Make the site **responsive** across screen sizes.
4. Add a **floating top menu**.
5. Add a **bottom banner**: "designed by Fernando Meneses, assisted by Claude Code".
6. May change `README.md` + `_config.yml`/theme, as long as it stays **GitHub Pages compatible**.
7. If using colors/boxes/decoration, a main color must be **green ≈ `#169903`**.

### Hard constraints (must not break)
- Free hosting on GitHub Pages.
- Lightweight & fast to load.
- Google Analytics tracking preserved (`G-BFPGQJLFVK`).

---

## 2. Current state (what I found)

- **Jekyll + remote theme**: `remote_theme: pages-themes/slate@v0.2.0`.
- **Content source**: `README.md` is rendered as the homepage (no `index.*` in root), wrapped by `_layouts/default.html`.
- **Layout**: `_layouts/default.html` is the stock Slate layout (header / single narrow `#main_content` column / footer). The narrow column you dislike comes from Slate's CSS `max-width` on `#main_content`.
- **Includes**: `_includes/head-custom.html` loads `_includes/head-custom-google-analytics.html` (GA tag) and a favicon line.
- **`ideas_html/`**: a scraped third-party site (NAIDOC, Drupal). Not your work — I will **ignore/leave it untouched** and not depend on it. **HUMAN COMMENT:** ignore ideas_html/.
- **Content sections** (top-level `#` headings → menu targets):
  Core competencies · CV and links · Career trajectory · Research AI-Projects · Coding challenges · Media releases · Scientific Publications · Image Gallery.
- Kramdown auto-generates heading IDs (e.g. `# Career trajectory` → `id="career-trajectory"`), so anchor-based nav links work without editing the content.

---

## 3. Proposed approach

### Recommended: replace the remote theme with a self-contained custom layout + CSS

Drop `remote_theme` and ship our own `_layouts/default.html` + a single small CSS file. Jekyll still renders `README.md` → HTML, so **content stays where it is**.

**Why this over keeping Slate + overriding it:**
- The narrow-column problem is baked into Slate's CSS; we'd be fighting `!important` overrides. A clean layout is simpler and more maintainable.
- **Faster load**: no remote theme fetch at build; one small local stylesheet, no JS frameworks.
- Full control over the floating menu, responsive grid, animations, and green accent.
- Still 100% GitHub Pages compatible (core Jekyll + kramdown only; no extra plugins).

**Alternative (lower change, kept on record):** keep Slate and override via `head-custom.html` + custom CSS. Rejected as the default because it's harder to make wide/responsive cleanly, but available if you prefer minimal change.

> **Decision needed from you:** approve the recommended approach (custom layout, no remote theme), or ask me to use the lower-change alternative.

**HUMAN ANSWER:** I approve the recommended approach.

---

## 4. Planned changes (file by file)

1. **`_config.yml`**
   - Comment out / remove `remote_theme` and the `jekyll-remote-theme` plugin.
   - Keep `title`, `description`, `email`, `google_analytics`, etc. unchanged.
   - Fix minor mismatch: `logo: assets/logo.png` points to a missing file (actual: `assets/logo_image.png`). Will correct or drop. **HUMAN ANSWER:** I approve the recommended approach. **HUMAN COMMENT:** the website logo is assets/website_icon_FM.png. I'm not sure what assets/logo.png was intended to.
   - **RESOLVED:** the actual file on disk is `assets/website_icon_FM.jpg` (extension is `.jpg`, not `.png`). I'll set `logo: assets/website_icon_FM.jpg` and use it as the favicon + nav logo. `assets/logo.png` doesn't exist → its reference is removed. `assets/logo_image.png` (used in the intro) does exist and stays.

2. **`_layouts/default.html`** (rewrite, self-contained)
   - `<head>`: viewport meta, link to new CSS, keep `{% seo %}` and `{% include head-custom.html %}` (preserves GA + favicon).
   - **Floating top nav**: fixed/sticky bar with the site title + anchor links to the 8 sections; smooth scroll; collapses to a hamburger toggle on small screens (tiny vanilla JS, no library).
   - **Content container**: wider, centered `max-width` (≈ 1100–1200px) with comfortable line length for text; padded so wide screens are used without hurting readability.
   - **Footer banner**: "Designed by Fernando Meneses, assisted by Claude Code." + existing GitHub Pages note.
   - Small inline `<script>` (≈30 lines) for: mobile menu toggle, smooth scroll, and IntersectionObserver scroll-reveal.

3. **`assets/css/style.css`** (new, our own — replaces the remote theme stylesheet)
   - CSS custom properties for the palette; **green `#169903`** as primary accent (nav, links, heading underlines, buttons/boxes).
   - Responsive layout via CSS Grid/Flexbox + a few `@media` breakpoints (mobile / tablet / desktop / wide).
   - Section cards/spacing for readability; gallery & project areas can use a responsive multi-column grid to fill wide screens.
   - Lightweight scroll-reveal animation classes (fade/slide-in) honoring `prefers-reduced-motion`.
   - System font stack (no web-font download) to keep it fast.

4. **`_includes/head-custom.html`**
   - Leave GA include intact. Possibly tidy the malformed favicon `<link>` line. No tracking changes.

5. **Content (`README.md`)**
   - Goal: **no structural rewrite required**; nav targets rely on existing headings.
   - Possible light touch-ups only if needed for layout (e.g. wrapping the project/gallery image groups so the grid looks good). Any such change will be listed before I make it.

### Explicitly unchanged
- All of `assets/` images, `CV_MENESES.pdf`, favicon.
- Google Analytics ID and behavior.
- Hosting model (GitHub Pages, free).
- `ideas_html/` (left as-is).

---

## 5. Animations (kept intentionally light)
- **Scroll-reveal**: sections fade/slide in once as they enter the viewport, via `IntersectionObserver` (native, ~20–30 lines, no dependency).
- **Nav**: subtle background/shadow change on scroll; smooth-scroll to anchors.
- **Hover**: small transitions on links/buttons/cards.
- Respect `prefers-reduced-motion: reduce` (disable for users who opt out).
- No animation libraries, no large GIFs.

## 6. Responsiveness
- Breakpoints roughly: ≤600px (mobile, hamburger menu, single column), 600–1024px (tablet), ≥1024px (desktop wide container), large screens capped for readability.
- Fluid images (`max-width:100%`), grid reflow for galleries/projects.

## 7. Color & style
- Primary accent: **`#169903`** (+ a darker/lighter green for hover/borders).
- Neutral light background, dark text for contrast/accessibility.
- Optional subtle boxes/cards with green accents for section separation.

---

## 8. Risks & mitigations
- **Heading IDs**: confirm kramdown slugs match nav anchors; if any differ I'll align the links (not the headings) — verified during local preview.
- **Removing remote theme** could drop styles content relied on → mitigated by the new self-contained CSS covering tables, lists, code, images.
- **GA regression**: untouched include; will verify the gtag snippet is present in built HTML.

## 9. How I'll verify before you publish
- Build/preview locally (`bundle exec jekyll serve`) if Ruby/Bundler available; otherwise validate the layout/CSS statically and describe what to check.
- Check: nav links jump correctly, layout is wide & responsive (resize), animations are subtle, footer banner present, GA tag in `<head>`, green accent applied.
- Commit on a branch and let you review the diff (and optionally a GitHub Pages preview) before merging to `main`.

## 11b. Content changes (from updated `planning_stage1.md`, lines 32–42)

These are **content edits to `README.md`**, on top of the layout work above.

### C1 — Core competencies (exact text edits)
- **Replace** the `⚙️ Machine Learning & AI` line with:
  `🤖 **Machine Learning & Agentic AI**: Deep learning | Claude Code | Spec-driven development | Computer vision | Time series forecasting`
  (note: emoji changes ⚙️→🤖; drops NLP & "Classical ML (scikit-learn)"; adds Claude Code & Spec-driven development.)
- **Replace** the `☁️ Cloud & Big Data` line with:
  `☁️ **Cloud & Big Data**: AWS | GCP | SQL`
- **Replace** the `🤝 Soft Skills` line with:
  `🤝 **Soft Skills**: Communication | Problem-solving | Project leadership | Project management | Teamworking`
- The other three lines (💻 Programming & Tools, 📊 Data Analysis, 📈 Visualization & BI) stay unchanged.

### C2 — Merge two sections into "AI-Projects and Challenges"
- Combine `# Research AI-Projects` and `# Coding challenges` into one top-level section **`# AI-Projects and Challenges`**.
- Keep every subsection and its content, in current order:
  Crypto Pipeline → Quantum Sensing & ML → AI assisting Quantum Noise Spectroscopy → Titanic → Spaceship Titanic → Open coding challenge: Bottle sets.
- **Menu impact:** the top menu drops from 8 → **7 items**:
  Core competencies · CV & links · Career trajectory · **AI-Projects and Challenges** · Media releases · Scientific Publications · Image Gallery.

### C3 — Scientific Publications → compact & graphical
- Current: a long bulleted list of ~13 papers + PhD thesis + degree project (title, venue, year, link). Section is now "less important", should be **space-limited and more graphical**.
- The papers have **no individual images/thumbnails**, so an image carousel/tile-gallery would need invented artwork. My recommendation avoids that:
  - **Recommended — compact "publication tiles" grid:** a responsive grid of small cards, each showing **venue + year** prominently with the **title revealed/expanded on hover (desktop) and tap (mobile/touch)**; the whole card links to the paper. Collapses the section to a fraction of its current height, looks graphical, needs only CSS + a few lines of JS, and stays accessible/SEO-friendly (titles remain in the DOM).
  - **Alternative — carousel/slider:** one paper visible at a time with prev/next. More "interactive" but hides most content, is heavier (more JS), and worse for accessibility/SEO. Kept on record.
  - The Google Scholar / ORCID / ResearchGate links stay (shown above or beside the grid).

> **Decision needed:** confirm **tiles grid (recommended)** vs **carousel** for Scientific Publications.
**HUMAN ANSWER:** tiles grid.

## 7c. Dark mode (added to this stage — HUMAN REQUEST)
- **Toggle** in the floating top nav (sun/moon icon) to switch light ↔ dark.
- **Default**: follow the OS via `@media (prefers-color-scheme: dark)`; the toggle overrides it.
- **Persistence**: remember the user's choice in `localStorage`.
- **No flash**: a tiny inline script in `<head>` sets the theme class before first paint (avoids a white flash on load for dark-mode users).
- **Implementation**: all colors driven by CSS custom properties; a `[data-theme="dark"]` block overrides the palette. Green accent `#169903` kept in both themes (slightly brightened in dark for contrast).
- Respects `prefers-reduced-motion`; theme transition kept subtle.

## 10. Out of scope (future stages)
- Content rewriting/copyediting, new sections, multi-page structure, blog. Can be Stage 2+ if you want.
- (Dark mode moved **into** this stage per your request — see §7c.)

---

## 11. Open questions for you
1. Approve the **recommended approach** (custom layout, drop remote theme) or use the **lower-change alternative** (keep Slate + overrides)?
**HUMAN ANSWER:** yes, I approve.
2. Exact **banner wording** — proposed: *"Designed by Fernando Meneses, assisted by Claude Code."* OK, or reword?
**HUMAN ANSWER:** OK.
3. Should I **work on a branch + PR** for review, or commit directly to `main`?
**HUMAN ANSWER:** work on main.
4. Any sections you want **excluded from the top menu** (8 items can get crowded on mobile — I can group some)?
**HUMAN ANSWER:** I added changes in @planning_stage1.md, read them.
