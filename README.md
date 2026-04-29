# Orderly DEX Template

A white-label perpetual futures DEX frontend built on the [Orderly Network](https://orderly.network) SDK. Fork this repo, edit `.env`, and deploy your own branded trading UI.

## Quick Start

1. Fork this repo
2. Edit `.env` — every variable is self-documented with inline comments
3. Install and run:

```sh
yarn install
yarn dev        # http://localhost:5173
```

## Configuration

**All configuration lives in `.env`.** Open it — every variable has comments explaining what it does, valid values, and defaults. There's no separate config file to hunt for.

Key things to set:

| Variable | Purpose |
|----------|---------|
| `VITE_ORDERLY_BROKER_ID` | Your Orderly broker ID (use `"demo"` for sandbox) |
| `VITE_ORDERLY_BROKER_NAME` | Display name shown throughout the UI |
| `VITE_APP_NAME` | Browser tab title and PWA name |
| `VITE_WALLETCONNECT_PROJECT_ID` | Get one at [cloud.walletconnect.com](https://cloud.walletconnect.com) |

### Theme

Colors are CSS custom properties in `app/styles/theme.css`. Edit directly or use the [Storybook theme editor](https://storybook.orderly.network/?path=/story/package-trading-tradingpage--page) to generate values.

### Logos

Place your logos in `public/`:
- `logo.webp` — primary logo (desktop nav)
- `logo-secondary.webp` — secondary logo (mobile nav)

Then enable them in `.env`:
```
VITE_HAS_PRIMARY_LOGO=true
VITE_HAS_SECONDARY_LOGO=true
```

### Navigation

Control which pages appear with `VITE_ENABLED_MENUS` and add external links with `VITE_CUSTOM_MENUS`. See `.env` for full details.

## Build & Deploy

### GitHub Pages (default)

This repo includes a GitHub Actions workflow that auto-deploys on every push to `main` or `master`. It enables Pages automatically on first run — no manual setup needed.

Just fork, push to main, and it deploys. The deployed URL will be:

```
https://<github-username>.github.io/<repo-name>/
```

**Custom domain:** Create a `CNAME` file in the repo root with your domain, then set `VITE_BASE_URL=` (empty) in `.env`.

### Manual / other hosting

```sh
yarn build:spa      # outputs to build/client/
```

For subdirectory deployments, set `VITE_BASE_URL=/repo-name/` in `.env` before building. Serve `build/client/` with any static host, SPA fallback to `index.html`.

## Runtime Config (No Rebuild)

You can override any `.env` value at runtime by creating `public/config.js`:

```js
window.__RUNTIME_CONFIG__ = {
  VITE_ORDERLY_BROKER_ID: "your_broker_id",
  VITE_ORDERLY_BROKER_NAME: "Your Brand",
};
```

## Resources

- [Orderly Network Docs](https://orderly.network/docs/sdks)
- [Orderly JS SDK](https://github.com/OrderlyNetwork/js-sdk)
- [Storybook Theme Editor](https://storybook.orderly.network/?path=/story/package-trading-tradingpage--page)
