# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

This is the public website for Uninterrupted, a meditation app for iPhone and Apple Watch, served by GitHub Pages at <https://uninterruptedmeditation.com>. Read `README.md` first for the pages, the shared files and how the site is deployed.

The app itself is in `../uninterrupted` (private repo `corbinhesse/uninterrupted`). Its `README.md`, `GLOSSARY.md` and `docs/adr/` are the source of truth for what the app does. Check them before writing anything here that describes the app, and use the app's words from `GLOSSARY.md` (a session, Begin, Done; not "timer session" or "start").

## Commands

```bash
# Preview the site at http://localhost:8765 (also the "pages" configuration in .claude/launch.json)
python3 -m http.server 8765
```

There is no build, linter or test suite. Before declaring a change done, open each changed page in the preview, at phone width as well as desktop width, and click its links.

## Conventions

- Plain HTML and CSS only: no build step, no framework, no JavaScript, no web fonts, no external scripts, stylesheets or analytics. The privacy policy says the app has no tracking or third-party code, and the site keeps to the same promise.
- Each page is a folder with an `index.html`. Link between pages with relative paths (`../privacy/`), which work both on the domain and in the local preview.
- Each page keeps its CSS in its own `<style>`, with colors as custom properties on `:root`.
- The home page sits on the app's sky (`SkyBackground.swift` and "Gradients" in the app's `README.md`): the dawn gradient and its orange sun glow in light mode, the dusk gradient and its peach glow in dark mode, following the system's setting. Keep its colors in step with the app's.
- The privacy policy uses the same sky and colors as the home page, copied into its own `<style>`; change both together.
- The beta page is light only (`color-scheme: light`), in the app's sunrise colors: Plum `#6b3fa0` to Coral `#d4566e` (the Begin button's gradient).
- The changelog (`changelog/index.html`) uses the home page's sky, copied into its own `<style>` like the privacy policy's, with each TestFlight build in a white card that stays white in dark mode. A card's lines are that build's GitHub release notes in the app repo (`gh release view v<version>+<build>`, the "What to Test" text from `scripts/changelog.sh notes`), word for word. When `/testflight` uploads a build, add its card at the top.
- `icon.svg` is the app icon drawn as SVG; use it with `<img>` rather than pasting the logo's path into a page. `logo.svg` is the "um" line alone; the home page uses it as a CSS mask so it takes the app's logo color (deep plum `#4a2a7a` on dawn, white on dusk). If the logo changes in the app (`docs/architecture/app-icon.md` there), update `icon.svg`, `logo.svg`, `apple-touch-icon.png` and `favicon.png` together.
- Headings use SF Rounded, as the app does: `ui-rounded, "SF Pro Rounded", ...`. Only Safari knows `ui-rounded`; the named font covers other browsers on a Mac that has it installed.
- Most visitors arrive on an iPhone, from a text message or the App Store, so every page has to read well at phone width.
- The home page's two columns are the rows of the app's introduction, word for word (`Uninterrupted/Introduction/IntroductionPage.swift`): its first page on the left, without "All data stays on your device" (left out on purpose), and its Apple Health page on the right. When those rows change in the app, change them here. SF Symbols can't be used on the web (Apple licenses them for app interfaces only), so the icons are their nearest [Phosphor](https://phosphoricons.com) icons, Regular weight, kept unchanged in `icons/` beside Phosphor's MIT license (`icons/LICENSE.txt`, which must stay). To add one, copy its SVG from the `@phosphor-icons/core` npm package rather than drawing it.
- The home page's Begin button copies the app's (`SunriseButtonStyle`, `BeginView.glow`, `Begin/CuppedLine.swift`) on a slower 10s cycle, in CSS only. Its icon is one SVG path, the app's cup, arch and cup again; the dash length (the cup, 90.652) and the distance it slides (cup + arch, 154.447) are measured from that path, so if the cup's shape changes in the app, copy the new points and measure both lengths again.
- The home page says "Coming soon to the App Store". When the app is public, replace that line with a link to its App Store page.

## Privacy policy

`privacy/index.html` is the policy that the app's Settings and App Store Connect link to. Its URL, `/privacy/`, is built into the app, so never move or rename it. It must describe what the app actually does: when the app starts handling data differently, update the policy and its "Effective" date in the same change, and check the claims against the app repo rather than guessing.

## Deploying

Pushing to `main` publishes the site (GitHub Pages, deploy from a branch, `main` at the root). Don't delete `CNAME` (the custom domain) or `.nojekyll` (serves the files without Jekyll).

## Branches

Because `main` is the live site, make changes on a branch and merge them with a pull request. When a session's first change request comes in, create the branch from an up-to-date `main` before editing anything: `git switch main && git pull --ff-only origin main && git switch -c <short-descriptive-name>`. Never commit to `main` directly. If there are uncommitted changes, carry them onto the new branch rather than discarding them.

## Moving from uninterrupted-privacy

This repo replaces `corbinhesse/uninterrupted-privacy` (<https://corbinhesse.github.io/uninterrupted-privacy/>), which will be deleted. Until that's done, these still point at the old site and need moving to `https://uninterruptedmeditation.com/privacy/` (and `/beta/`):

- the privacy policy link at the bottom of the app's Settings, and the "Privacy policy" section of the app's `README.md`
- the Privacy Policy URL in App Store Connect
- the beta link already sent to testers

Delete this section once the old repo is gone.

## Shell & Environment

- The user's shell is fish, but the Bash tool runs **zsh**. Quote globs (`'*.html'`) and write commands in POSIX/zsh syntax, not fish syntax.
- This is macOS, which uses BSD sed (`sed -i '' ...`). Prefer the Edit tool for file edits.
- `.claude/settings.local.json` blocks the YNAB, Strava, Gmail, Google Calendar and Google Drive MCP servers for this repo. Don't use them here.
