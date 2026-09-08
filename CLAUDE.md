# CLAUDE.md

## Stack & Conventions

- **Single-file project.** The entire project must live in one `index.html`
  file, with all CSS and JavaScript inlined via `<style>` and `<script>`
  tags — never split into separate `.css`/`.js` files or additional HTML
  pages. Linking external images, CSS libraries, and JavaScript libraries
  (e.g. via `<link>`/`<script src="https://...">`) is allowed. This
  constraint exists so the finished project can be copy-pasted as a single
  file for sharing in class and on single-file code platforms.
- **Vanilla only.** Use plain HTML, CSS, and JavaScript only — no
  frameworks or libraries bundled into the project, and no build step
  (no bundlers, transpilers, or package managers required to run it).
  Open `index.html` directly in a browser and it must work.
