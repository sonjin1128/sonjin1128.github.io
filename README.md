# sonjin1128.github.io

Personal academic homepage of Sungjin Bae — a calm, single-page static site (plain HTML/CSS/JS, no build step). Hosted on GitHub Pages at <https://sonjin1128.github.io>.

## Structure

- `index.html` — the entire site (Hero · About · Research · Publications · CV · Contact)
- `DESIGN.md` — the design system all pages follow (colors, type, spacing, components)
- `assets/images/profile.jpg` — profile photo (web-optimized)
- `assets/media/` — put demo GIFs / videos for the Research cards here
- `.nojekyll` — tells GitHub Pages to serve files as-is (no Jekyll processing)

## How to update

Edit `index.html`, then commit and push in GitHub Desktop. Changes appear at the live URL within 1–3 minutes.

- Change the accent color: edit `--accent` in the `:root` block at the top of `index.html`
- Add a demo to a Research card: drop a file in `assets/media/` and replace the matching `card-media` div
