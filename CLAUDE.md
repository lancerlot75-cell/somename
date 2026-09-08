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

## Tech stack (hard constraints — do not deviate)
- Vanilla HTML, CSS, and JavaScript only. No React, Vue, or any JS framework.
- Tailwind CSS for all styling (via CDN only).
- No backend, no database. Fully static site.
- A toggle for light and dark theme, with the choice remembered
  across visits.

## Working conventions
- Before implementing any non-trivial feature, ask clarifying
  questions about scope, edge cases, and constraints first —
  don't propose a plan until you've asked.

## Feature Plan

Portal for browsing/trying a growing collection of small web
tools and learning artifacts. Everything lives in `index.html`;
tools are views within it, not separate pages.

**Data model — tool registry:** a JS array of
`{ id, title, description }` objects, one entry per tool. The
home grid and the router both read from this array. Adding a
future tool = one new registry entry + one new view `<section>`
— no shell rewrite.

**Key flows:**
- *Routing:* read `location.hash` on load and on `hashchange`.
  A hash matching a registry `id` shows that tool's `<section>`
  and hides the rest; no match (or empty hash) shows the home/
  catalog view. Each tool view has a "back to catalog" link.
- *Home view:* renders one card per registry entry (title +
  one-line description), linking to `#<id>`.
- *Theme toggle:* a toggle button flips a `dark` class on
  `<html>` (Tailwind's `dark:` strategy) and persists the choice
  to `localStorage`; the stored (or system) preference is
  applied before first paint to avoid a flash of the wrong theme.
- *Per-tool rendering:* each tool's Three.js scene/camera/
  renderer/animation loop is self-contained in its own `<script>`
  block. No shared rendering/control-panel abstraction yet —
  some duplication between tools is expected and fine until more
  tools exist and real commonality is clear.

### Phase 1 — Portal shell + 2 tools (1 of 2 tools done)
- **Shell — done.** `index.html` has the home/catalog view (card grid
  driven by the tool registry), hash-based routing between views, and
  a theme toggle persisted to `localStorage`.
- **Reciprocating pump visualizer — done.** Real Three.js scene with
  OrbitControls: sliders for crank speed (RPM), stroke length, and
  connecting rod length drive slider-crank kinematics in real time,
  animating the crank arm, connecting rod, and piston. Two valve
  indicators at the cylinder head switch between intake/discharge based
  on piston velocity direction; a readout panel shows live crank angle,
  piston position/velocity, and stroke phase.
- **Four-bar linkage / cam mechanism visualizer — not started.** Real
  Three.js scene: inputs for link lengths (or cam profile); animates
  the linkage motion in real time.

### Added outside Phase 1 — Hydraulic Sequencing Circuits
- **Done.** A third tool (not part of the original Phase 1 list): a 2D SVG
  step-through simulator covering two sequencing circuits — a mechanical
  (pilot-operated) sequence valve circuit (STAMP/CLAMP) and a pressure
  sequencing valve circuit (A/B). Each circuit's content is followed by an
  inline check-in question (shows right/wrong, then a Continue button reveals
  the next part regardless of the answer), and the tool ends with a 3-question
  quiz.

### Later phases (not yet planned in detail)
- More tools/lessons: extend the registry + add a view section
  per tool.
- Revisit whether shared rendering/control-panel helpers are
  worth extracting once several tools exist.
