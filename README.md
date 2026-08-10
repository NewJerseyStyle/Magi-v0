# MAGI SYSTEM — single-file web app

One HTML file, all animations and the debate engine intact. Talks to any
OpenAI-compatible chat completions endpoint (`base_url` + API secret key).

## How to use

1. Open `magi.html` in a browser (double-click, or serve it:
   `python -m http.server 8000` then visit http://localhost:8000/magi.html)
2. Fill in the setup panel:
   - **Base URL** — your endpoint root, e.g. `https://api.example.com/v1`
   - **API key** — your secret key
   - **Model** — e.g. `gpt-4o-mini`, `Grok-4.1-Fast-Reasoning`, etc.
3. Click “Initialize Connection”, then enter a topic and run the debate.

Credentials are kept only in the browser (localStorage) and are sent straight
to your endpoint from the browser. Nothing is stored on any server.

## If the browser blocks the request (CORS)

Most browsers block cross-origin `fetch` from `file://` pages or when the
endpoint does not send CORS headers. Options:

- Serve this page over http and pass credentials in the URL once:
  `?base=https://...&key=sk-...&model=...` (nothing is saved in that case)
- Or enable CORS on your LLM gateway (e.g. LiteLLM `--enable-cors`)

## Details

- OpenAI JS SDK is lazy-loaded from a CDN; if it cannot load (offline or
  `file://`), the app falls back to a raw `fetch` + SSE parser automatically.
- `marked` renders the deliberation entries as markdown; it also degrades
  gracefully when offline.
- Dark mode follows your OS setting.

