# E-ink PR Viewer

## Target Display

This project is optimized for the **Boox Kaleido 3** color e-ink display.

### Kaleido 3 Display Characteristics

- Color e-ink using color filter array (CFA) on top of monochrome e-ink
- Resolution: ~300 PPI for black/white content, ~150 PPI effective for color
- Color rendering: limited saturation, somewhat muted — bold/saturated colors work better than pastels
- No backlight by default (front-lit optional)
- Refresh: full refresh causes flash; partial refresh is used for UI updates
- Color gamut is significantly smaller than LCD — avoid subtle color distinctions

### Design Constraints

- **No animations or transitions** — e-ink cannot render them cleanly
- **No shadows or gradients** — use solid borders instead
- **High contrast** — black text on white background for body content
- **Limited color palette**: use color only for status indicators:
  - `#cc0000` red → failure / error / deletions
  - `#006600` dark green → success / additions
  - `#000000` black / `#ffffff` white → primary content
  - `#444444` muted gray → secondary/metadata text
  - `#f0f0f0` light gray → backgrounds for headers/code blocks
- **Avoid green for large areas** — Kaleido color fidelity varies; prefer black/white for structure
- **Bold, readable fonts** — Georgia serif for body, Courier monospace for code/meta
- **Minimum 18px body font** — e-ink pixel rendering benefits from larger type
- **Thick borders** (2px+) — thin lines can disappear on e-ink

### Architecture Notes

- Single HTML file (`index.html`) — no build step, no dependencies
- Fetches directly from GitHub REST API (v3) from the browser
- Token stored in-memory only (password input), never persisted
- `localStorage` persists only: repo name and PR state filter
