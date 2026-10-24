# Orbit Voice HUD — Meta Ray-Ban Display Web App

A dependency-free, single-file web app designed for the Meta Ray-Ban Display glasses. All three controls work as buttons, and it registers three optional WebMCP tools on compatible glasses:

- `activate_hud`: show the custom heads-up display
- `start_timer`: start a countdown (default 5 minutes, optional duration 1–180 minutes)
- `show_notes`: open the note viewer/editor

## Run locally

Open `index.html` in a desktop browser for a quick manual test. For local HTTP testing, in this folder run `python -m http.server 8080` and open `http://localhost:8080`.

## Use on the glasses

1. Deploy `index.html` to an HTTPS web host (e.g. GitHub Pages or another static host). No build step or API keys needed.
2. Enable Developer Mode for web apps in the Meta AI app. Add your HTTPS URL as a web app to your Meta Ray-Ban Display glasses.
3. Launch the web app on the glasses. Navigate via the Meta Neural Band / D-pad or voice if WebMCP is enabled on your device.
4. Try "Hey Meta, activate HUD", "Hey Meta, start a timer for five minutes", or "Hey Meta, show notes". The Meta AI WebMCP integration is in developer preview and might not be enabled for every device.

The app shows whether WebMCP tool registration succeeded at the top. The interface remains functional without voice support. The `registerTool` implementation follows the current `document.modelContext.registerTool` WebMCP approach; it does not attempt to replace Meta's wake phrase or change built-in glasses settings.

## Limitations

- Browser notes use localStorage, so they may differ across phone, desktop, and glasses. This app does not synchronize them.
- Timer works while the app remains active; browser/OS suspension may prevent a live alert, but it uses a real end timestamp and catches up when resumed.
- Tool registration does not prove Meta AI has access on a specific device; voice invocation requires Meta's rollout / Developer Mode and an open compatible app.
- User text can be entered through whatever dictation/keyboard features the device exposes; the app does not directly listen to the glasses microphone.

## References

- https://developers.meta.com/wearables/web-apps/
- https://developers.meta.com/wearables/faq/
- https://github.com/facebook/meta_glasses_webmcp
- https://github.com/webmachinelearning/webmcp
