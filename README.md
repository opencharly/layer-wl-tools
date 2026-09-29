# layer-wl-tools

Compositor-agnostic Wayland/X desktop-automation CLI tools for OpenCharly desktop
images.

The `wl-tools` candy installs the wlroots input/clipboard/window toolset —
`wtype`, `wl-clipboard` (`wl-copy`/`wl-paste`), `wlr-randr`, `wlrctl`, `xdotool`,
`ydotool`, plus the `xprop`/`xwininfo` X utilities — used to drive and introspect
a Wayland desktop. It backs the `wl:` check verb on wlroots compositors (sway,
labwc) and, via `kdotool`, partially on KWin. Screenshots are **not** included;
use `wl-screenshot-grim` (sway) or `wl-screenshot-pixelflux` (selkies).

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `wl-tools` |
| Packages | `wtype`, `wlrctl`, `xdotool`, `xprop`/`xorg-xprop`, `xwininfo`/`xorg-xwininfo`, `wl-clipboard`, `wlr-randr`, `ydotool` |
| Binaries | `/usr/bin/{wtype,wl-copy,wl-paste,wlrctl,wlr-randr,xdotool,ydotool}` |
| Depends | none (compositor-agnostic) |
| Service / port | none |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list — typically
transitively through the `sway-desktop` or `selkies-desktop` metalayer. The
named entity is a box: its `candy:` value is the box BODY (holding `base:` and
the nested composition `candy:` list):

```yaml
my-desktop-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-wl-tools:v2026.240.0121'
```

Then drive the desktop through the `wl:` check verb (run with `charly check live
<image> --filter wl`):

```bash
wtype "hello"                 # Wayland-native keyboard input
wl-copy "text" && wl-paste    # clipboard
wlrctl window list            # wlroots window management
```

On KWin the `wl:` verb is compositor-aware and routes window management through
`kdotool`; the wlroots-backed tools fail-fast with an "unsupported on KWin"
error rather than hanging.

The candy's `plan:` asserts each tool's binary on PATH under `/usr/bin`.

## Layout

- `charly.yml` — the `wl-tools:` candy entity (the per-distro packages, including
  the AUR `wlrctl` on Arch, the `check:` assertions) and the embedded
  `wl-tools-skill:` skill entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-selkies:wl-tools`
- `/charly-check:wl` — the `wl:` check verb that uses these tools (routes per compositor: wlroots via these tools, KWin via `kdotool`)
- `/charly-selkies:kde-shell` — KDE Plasma session candy that ships `kdotool`
- `/charly-selkies:wl-screenshot-grim` — screenshot candy for sway (grim)
- `/charly-selkies:wl-screenshot-pixelflux` — screenshot candy for selkies (also the KWin screenshot path)
- `/charly-selkies:sway-desktop` / `/charly-selkies:selkies-desktop-layer` — metalayers that include this candy
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
