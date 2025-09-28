# VATSIM-data — Local dev

This repo contains a single `index.html` which fetches the VATSIM controllers feed.

If you see a CORS or network error when opening the file directly from the filesystem, run the tiny Node static server included here which also provides a proxy endpoint to the controllers feed to avoid CORS during development.

Requirements
- Node.js 16+ (for `node-fetch`)

Quick start

1. Install dependencies:

```powershell
npm install
```

2. Start the server:

```powershell
npm start
```

3. Open http://localhost:8000/index.html in your browser.

Notes
- The server serves static files from the repository root and exposes `/proxy/controllers.json` which proxies the live feed.
- `index.html` fetches the feed directly; if your browser still runs into CORS when fetching the original URL, you can manually edit the `URL` constant in `index.html` to `/proxy/controllers.json` to use the proxy.

- `artccs.json` is an optional config used to render ARTCC tiles. Each entry can be:

```json
{ "code": "ZBW", "name": "Boston ARTCC", "aliases": ["BOS", "ZBW1"] }
```

The UI will show the primary `code` on the tile but will filter items matching the primary code or any `aliases`.

- `overrides.json` is an optional file to map controller callsigns to short role abbreviations. Example:

```json
{
	"overrides": {
		"EXAMPLE1": "S1",
		"EXAMPLE2": "APP"
	}
}
```

When present, `index.html` will use the override for the callsign (case-insensitive) and display the abbreviation after the controller's name, e.g. "Jane Doe - S1".
