# Orbit AI v4.3

A static, responsive AI interface with a custom Three.js holographic orb, shader-driven animated background, and browser-persisted conversation history.

## Run locally

Serve this directory over HTTP (ES modules and WebGL work best from an HTTP origin):

```sh
python3 -m http.server 8000
```

Then visit `http://localhost:8000`. Three.js is bundled locally. The typeface loads from Google Fonts when online, with a local system-font fallback.

## Connect an AI backend

The app starts in clearly labeled local demo mode. To use an AI provider, set `apiUrl` in `app-config.js` to point to your own authenticated server endpoint. The empty default always uses local demo replies. The page sends:

```json
{"messages":[{"role":"user","content":"Hello"}]}
```

The endpoint can return JSON with a `reply`, `content`, or `text` field, or a text/event-stream response. Keep provider credentials on the server. The attachment control currently selects and displays a file in the interface; upload handling should be added to the backend contract before enabling document-aware answers.

## Included interactions

- Rotating, animated WebGL sphere and slowly evolving fluid shader background, with an animated CSS fallback for browsers where WebGL cannot start
- Cursor-responsive lighting, reduced-motion CSS support, and background rendering pause when the tab is hidden
- Auto-revealing desktop navigation and touch-friendly mobile conversation drawer
- Searchable, filterable conversations, title generation, deletion, clear-history confirmation, and localStorage persistence
- Enter to send, Shift+Enter for a newline, Ctrl/⌘+N for a new chat, and `/` to search
- File picker, browser speech recognition where available, theme toggle, and fullscreen control
- Settings drawer with Personalization preferences and Appearance palettes (Aurora, Emerald, Cosmic, Solar, Rose, Arctic, Citrus, Nebula), plus a custom fluid color; selections persist locally

## Sign-in options

The welcome screen offers guest entry and Google sign-in. Guest mode stores its choice in this browser and keeps conversations on this device. Google OAuth requires a server endpoint: set `googleAuthUrl` in `app-config.js` to your OAuth start endpoint. That endpoint must handle the OAuth flow and redirect back to this app; this static demo does not include a Google client ID, token validation, or authentication server.
