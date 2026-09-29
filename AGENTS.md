# AGENTS.md — layer-wl-tools

Standalone candy repo for the `wl-tools` layer — the compositor-agnostic
Wayland/X input, clipboard, and window tools that back the `wl:` check verb. The
candy lives in `charly.yml` at the repo root: the per-distro packages (including
the AUR `wlrctl` on Arch), the `check:` assertions, and the embedded `skill:`
entity projected into the marketplace corpus as `/charly-selkies:wl-tools`.

Canonical files:

- `charly.yml` — the `wl-tools:` candy entity and the `wl-tools-skill:` skill
  entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-selkies:wl-tools` — the owning skill. The tool-to-protocol map, the
  wlroots-vs-KWin compatibility table, and the `wl:` verb integration. Load
  before editing or troubleshooting the layer.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:`, per-distro `distro:` arms, package/repo
  sections, service declarations). Load before editing any entity field or plan
  step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps are the functional evidence — each tool's
  binary on PATH.
- Package names diverge per distro (`xprop` vs `xorg-xprop`, `xwininfo` vs
  `xorg-xwininfo`) and `wlrctl` ships from the AUR on Arch; keep every arm in
  sync when adding a tool.

## Modify this repo

- Edit the `wl-tools:` candy entity AND the `wl-tools-skill:` skill entity in
  `charly.yml` together. The skill is the projected usage source, so a behaviour
  change not mirrored in the skill leaves the corpus stale.
- Adding a tool means: the per-distro package, the `check:` binary assertion, and
  the skill's tool table, in the same change.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- PR-only. Every change lands through a pull request; the org-required
  `charly/pr-validator` validates the diff and body and arms native auto-merge on
  PASS. Direct pushes to `main` are blocked.
- History lives in `CHANGELOG/` (written by `tag-on-merge` at merge time); the PR
  body IS the changelog.
- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo. Do not
  restate its rules here.
