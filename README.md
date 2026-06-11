# 🎂 Birthday Celebration

An interactive birthday experience — enter a name and age, make a wish,
and blow out the candles **with your actual breath** (microphone-based
blow detection), followed by fireworks, music, gifts, and more.

## What's inside

```
birthday-celebration/
├── index.html              ← Vite entry
├── package.json
├── vite.config.js
├── src/
│   ├── main.jsx
│   └── App.jsx             ← the entire app (single component file)
└── standalone/
    └── birthday-celebration.html   ← zero-install version (React via CDN)
```

## Option 1 — Run the Vite app (recommended)

Requires Node.js 18+.

```bash
npm install
npm run dev
```

Open the printed URL (usually http://localhost:5173).

Production build:

```bash
npm run build      # outputs to dist/
npm run preview    # serve the production build locally
```

## Option 2 — Zero-install standalone file

No Node needed — just serve the `standalone/` folder with any static server:

```bash
cd standalone
npx serve .                  # or: python3 -m http.server 8000
```

Then open http://localhost:3000/birthday-celebration.html
(or http://localhost:8000/... for the Python server).

> Don't open the file directly via `file://` — the microphone won't work.

## 🎤 Microphone (blow detection) requirements

`getUserMedia` only works in a **secure context**:

- ✅ `http://localhost` (any port)
- ✅ Any `https://` URL
- ❌ `file://` opened directly
- ❌ LAN IPs like `http://192.168.x.x` (browsers treat these as insecure)

**Testing on your phone:** tunnel your local server to get an https URL:

```bash
ngrok http 5173        # (or 3000/8000 depending on your server)
```

Open the https ngrok URL on your phone, allow mic access, and blow. 💨

If detection feels too eager or too stubborn, use the **Sensitivity**
slider under the mic meter. The "Blow candles manually" button is always
there as a fallback.

## Deploying (to actually gift it)

The easiest path is Vercel or Netlify:

```bash
npm run build
# then drag the dist/ folder into Netlify, or:
npx vercel
```

Mic works out of the box on the deployed https URL — just send the link.

## Notes

- The Happy Birthday melody is generated programmatically with the
  Web Audio API (no audio files needed).
- Memory wall notes are session-only (in-memory).
- 4 themes via the dots in the top-right corner.
- Respects `prefers-reduced-motion`.
