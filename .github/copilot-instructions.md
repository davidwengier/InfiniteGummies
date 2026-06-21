# Infinite Gummies instructions

Infinite Gummies is a static, GitHub Pages-friendly clicker game. Keep the app simple: `index.html` contains the HTML, CSS, and JavaScript, and `Dug.png` is the only image asset currently required outside that file.

## Project context

- Theme: gummy snake / Australian lolly clicker game. Prefer "lolly" / "lollies" for general candy wording, and "gummy snake(s)" for the main currency.
- The visible game name is **Infinite Gummies**.
- The final building is **Dug**, using the committed `Dug.png` asset.
- The app saves progress in `localStorage` using `gummy-snake-clicker-save-v1`; dark mode uses `infinite-gummies-theme`.
- Ascension grants 1 gummy snake head per billion gummies earned in the current run, then resets run upgrades/buildings while preserving permanent head-shop upgrades.
- The game is intended to be hosted directly from the repository root on GitHub Pages.

## Implementation conventions

- Do not introduce a build system or package manager unless the user explicitly asks for one.
- Keep changes in plain HTML/CSS/JavaScript in `index.html` where possible.
- Building and upgrade definitions live in JavaScript arrays; update the render helpers when changing any displayed rate, cost, owned count, or effect.
- Preserve existing save compatibility where practical. Existing saves may contain older `upgrades` data that is mapped into `buildings`.
- Keep mobile play usable: avoid double-tap zoom regressions and keep the click target responsive.
- Keep the left click panel sticky on desktop and usable on mobile.

## Local development

Run the site locally from the repository root with:

```powershell
dnx dotnet-serve --port 8080 --directory .
```

Then open `http://localhost:8080/`.

Before finishing code changes, at minimum parse the inline script:

```powershell
node -e "const fs = require('fs'); const html = fs.readFileSync('index.html', 'utf8'); const start = html.indexOf('<script>') + '<script>'.length; const end = html.indexOf('</script>'); new Function(html.slice(start, end)); console.log('Parsed inline script.');"
```

## Git notes

- Repository: `https://github.com/davidwengier/InfiniteGummies`
- Main branch: `main`
- This repo's local git `user.email` should be `git@wengier.com` before committing.
