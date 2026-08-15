# Portfolio — Maddie Reardon (Technical Writing)

Technical writing portfolio site for Maddie Reardon, senior technical writer. Static HTML, no build step, no dependencies. Sibling site to [learning-portfolio](https://maddie35.github.io/learning-portfolio/), which covers the learning design side of the practice.

## Pages

| File | Purpose |
| --- | --- |
| `index.html` | Home, with the samples index and "How I work" |
| `samples.html` | All five samples, sorted by the problem solved |
| `about.html` | Background, track record |
| `request-access.html` | How to request the two client-owned locked samples |
| `sample-affirm.html` | Sample — Affirm checkout documentation (excerpt) |
| `sample-black-holes.html` | Sample — Introduction to black holes (full explainer) |
| `sample-information-architecture.html` | Sample — Affirm developer docs IA overhaul |
| `sample-manage-connections.html` | Sample — Manage connections help topic |

`assets/styles.css` holds the design tokens and component classes (`.blueprint`, `.btn`, `.tag`, `.card`). It is the same "Industry" design system used by the learning-portfolio site — retune variables in `:root` rather than overriding at the page level.

## Local preview

```bash
python3 -m http.server 8000
```

Then open <http://localhost:8000>. Opening the files directly with `file://` also works, since there is no JavaScript.

## Publishing with GitHub Pages

Push this folder as the root of `github.com/maddie35/portfolio`, then Settings → Pages → Source: *Deploy from a branch* → `main` / `/ (root)`.

The site will be served at `https://maddie35.github.io/portfolio/`. `.nojekyll` is included so Jekyll does not reprocess the files.

## Notes on the export

This originated as a Claude Design project ("UI mockups for technical writing portfolio"), a canvas with several explored directions. The implemented pages are the ones the canvas's final turn ("The direction we're keeping") kept: home and samples-index layouts from that turn, plus the four sample/about/request pages it linked out to from the prior turn.

Conversion notes:

- **The React runtime was removed**, same as learning-portfolio: pages no longer wrap markup in `<x-dc>` / load `support.js`.
- **Canvas-only template placeholders were resolved to static values.** `{{ indexCols }}` became a fixed 5-column grid on the samples index; `{{ showThumbnails }}` / `<sc-if>` wrappers were resolved to "always show" (thumbnails are always rendered); `{{ portraitOpacity }}` became `.15`, matching the duotone opacity used elsewhere on this site; `{{ portraitRatio }}` on the About page portrait became `3/4`.
- **Anchor-based canvas navigation (`#3a`, `#2h`, etc.) was converted to real pages.** The nav's "Method" link, which pointed at the canvas's Home turn, now points to `index.html#how-i-work`, the section it was meant to reach.
- **Every page got its own header/footer nav**, since the canvas assumed all options lived on one scrollable page with shared chrome. `sample-black-holes.html` keeps the distraction-free reading header from its own design option instead.
- **`lang="en"`, `<title>`, and meta descriptions were added**, as the exported canvas had none.

## Known trade-offs

- Several images (portrait, before/after IA screenshots, an MP4 walkthrough, and the "Manage connections" mobile screenshots) are still referenced from their original external hosts (S3, GitHub user-content) rather than copied into `uploads/`. Worth mirroring locally if those hosts are not guaranteed to stay up.
- `sample-affirm.html` links out to `https://maddie35.github.io/portfolio/TECH-DOC` for "the full sample" — that page doesn't exist in this repo yet.
- `request-access.html` doubles as the sitewide "Get in touch" destination (every "Get in touch" button points here), even though its content is scoped to the two locked samples. That's how the source design wired it; worth revisiting if a general contact page is wanted later.
