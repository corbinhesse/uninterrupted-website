# Uninterrupted website

The public website for Uninterrupted, a meditation app for iPhone and Apple Watch, at <https://uninterruptedmeditation.com>. It is plain HTML and CSS, with no build step, no JavaScript and no third-party code.

## Pages

| URL | File | What it is |
|---|---|---|
| `/` | `index.html` | What the app is |
| `/privacy/` | `privacy/index.html` | The privacy policy, linked from the app's Settings and from App Store Connect |
| `/beta/` | `beta/index.html` | How friends and family join the TestFlight beta (not linked from the other pages) |
| `/changelog/` | `changelog/index.html` | What changed in each TestFlight build, one card per build (not linked from the other pages) |

Each page is a folder with an `index.html`, so its URL has no `.html` on the end. The files the pages share sit at the root: `icon.svg` (the app icon), `logo.svg` (the "um" line on its own), `icons/` (the home page's icons, from [Phosphor](https://phosphoricons.com) under the MIT license in `icons/LICENSE.txt`), `apple-touch-icon.png` (the icon iPhones show in link previews and on the Home Screen) and `favicon.png`.

## Preview

```bash
python3 -m http.server 8765
```

Then open <http://localhost:8765>. Links between pages are relative (`../privacy/`), so they work the same here as on the domain.

## Deploying

GitHub Pages serves the `main` branch from the root of the repo (**Settings › Pages › Deploy from a branch**). A push to `main` is live within a minute or two.

- `CNAME` holds the custom domain, `uninterruptedmeditation.com`. Pages reads it from the branch, so don't delete it.
- `.nojekyll` tells Pages to serve the files as they are, without running Jekyll.

The domain is registered with Squarespace. Its DNS points at GitHub Pages:

| Host | Type | Value |
|---|---|---|
| `@` | A | `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153` |
| `@` | AAAA | `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153` |
| `www` | CNAME | `corbinhesse.github.io` |

## History

The privacy policy and the beta page used to live in [`uninterrupted-privacy`](https://github.com/corbinhesse/uninterrupted-privacy), published at <https://corbinhesse.github.io/uninterrupted-privacy/>. This repo replaces it.
