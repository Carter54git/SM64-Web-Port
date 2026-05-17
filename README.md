# Super Mario 64 — Web Edition

Browser-based port of Super Mario 64 for the Nintendo 64, delivered as a static site using WebAssembly and WebGL. The game loads on demand after the start screen and runs without a native install.

## Features

- WebAssembly runtime (`sm64.wasm`) with Emscripten glue code (`sm64.js`)
- Start screen with control reference before the game loads
- Russian and English UI on the start screen (RU / EN toggle, preference stored in `localStorage`)
- Keyboard, on-screen touch controls (mobile), and gamepad support (Gamepad API)
- Mobile layout: fixed render buffer, viewport-aware scaling, landscape hint
- GitHub Pages–ready deployment (static files only, no build step)

## Live demo

After you enable GitHub Pages, set the site URL here:

`https://<username>.github.io/<repository>/`

## Requirements

| Target | Minimum |
|--------|---------|
| Browser | Recent Chromium, Firefox, or Safari with WebAssembly and WebGL |
| Desktop | Keyboard; optional gamepad |
| Mobile | Touch screen; landscape orientation recommended |
| Hosting | Static file server; `application/wasm` MIME type for `.wasm` files |

GitHub Pages serves `.wasm` correctly when a `.nojekyll` file is present in the site root (included in this repository).

## Controls

### Desktop (keyboard)

| Input | Action |
|-------|--------|
| Arrow keys | Move |
| X | Jump |
| C | Punch / pick up |
| Z | Crouch / wing cap flight |
| Enter | Pause / confirm |
| W A S D | Camera |

### Gamepad

| Input | Action |
|-------|--------|
| Left stick / D-pad | Move |
| A | Jump |
| B / R1 | Z |
| X / L1 | Punch |
| Start | Pause |
| Right stick | Camera |

### Mobile (touch)

Virtual stick (movement), action buttons (X, C, Z, Start), and camera pad (bottom right). Hold the device in landscape for the best experience.

## Local development

No build step is required. Serve the repository root over HTTP (opening `index.html` directly from the file system may block WebAssembly).

**Python 3:**

```bash
python -m http.server 8080
```

Open `http://localhost:8080/` in your browser.

**Node.js (npx):**

```bash
npx --yes serve .
```

## Deploy to GitHub Pages

1. Create a new repository and push this project to the `main` branch.
2. In the repository: **Settings → Pages → Build and deployment**.
3. Set **Source** to **GitHub Actions**.
4. Push to `main`. The workflow in `.github/workflows/pages.yml` publishes the site.
5. After the workflow succeeds, open the URL shown under **Settings → Pages**.

The workflow uploads the repository root as the site artifact (`index.html`, `sm64.js`, `sm64.wasm`, and supporting files).

## Project structure

```
.
├── index.html          # UI shell, input handling, i18n, mobile scaling
├── sm64.js             # Emscripten module loader and runtime hooks
├── sm64.wasm           # Game binary (WebAssembly)
├── .nojekyll           # Required for GitHub Pages (WASM and static assets)
├── LICENSE             # MIT (web shell; see Legal notice)
├── THIRD_PARTY.md      # Emscripten and other attributions
└── .github/workflows/
    └── pages.yml       # GitHub Pages deployment
```

## Legal notice

**Super Mario 64** and related trademarks are property of **Nintendo Co., Ltd.** This repository is an independent fan project and is **not** affiliated with, sponsored by, or endorsed by Nintendo.

- Do not use this project to imply official Nintendo distribution or support.
- You are responsible for compliance with applicable copyright and trademark laws in your jurisdiction before publishing or sharing a fork.
- Game logic and assets embedded in `sm64.wasm` remain subject to the rights of their respective owners.

Use at your own risk. The maintainers provide no warranty (see `LICENSE`).

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Bug reports and pull requests are welcome for the web shell (`index.html`) and deployment configuration. Changes that require rebuilding `sm64.wasm` should document the toolchain and source revision used.

## Security

To report a security issue, see [SECURITY.md](SECURITY.md).

## License

The web shell and repository metadata are licensed under the [MIT License](LICENSE). Third-party components are described in [THIRD_PARTY.md](THIRD_PARTY.md).
