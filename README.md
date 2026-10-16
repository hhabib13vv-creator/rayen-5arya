# Rayen Bitch Game — Cursed Pixel Adventure

A static browser platformer made as a chaotic best-friend gift for **Rayen**. Pixel-art game, three stages, a boss, dialogue, music, and a Meme Lab for the photos.

## Run it

**Easiest:** double-click `index.html` (Chrome on Ubuntu works) — photos load from the `photos/` folder, no server needed.

Or serve it (also how it works on GitHub Pages / any static host):

```bash
python3 -m http.server 8000     # then open http://localhost:8000
```

Keep the folder structure intact: `index.html`, `game.js`, `style.css`, `custom-content.json`, `custom-content.js` and the `photos/` folder must stay together.

## Photos

- Your 12 original photos are in `photos/` as byte-for-byte originals (never resized, compressed, cropped or recoloured). A copy of your original base64 bundle is kept in `original/`.
- In the game they are drawn **small, smooth and proportional** (aspect ratio kept, contain-fit) inside a pixel-art frame; only the game art is pixelated, never the photos.
- **Order:** photos are handed out in editor order, one per collectible, and a photo only repeats after *every* loaded photo has been used. The final-reveal photo is held back for the ending, so one playthrough (5 + 6 collectibles + the reveal) shows all 12 photos once.
- The home screen and Meme Lab show a real count, e.g. `✔ PHOTOS: 12/12 loaded`, or `⚠ 11/12 loaded · FAILED: name.png`. A photo that fails to load is reported and skipped — never replaced by a fake.
- **Meme Lab:** large cards with the full photo (contain), original size, load status and where each is used; click one to view the original enlarged (← → to browse, Esc to close).

## How loading works (file:// and hosting)

`custom-content.json` is the photo list/captions/letter. Browsers block `fetch()` of local files on `file://`, so `custom-content.js` (generated from the JSON) is loaded with a normal `<script>` tag. On http(s) the JSON is fetched fresh; on file:// the script is used.

## Changing photos / publishing a new bundle

1. In Meme Lab add/reorder photos and click **Export custom bundle** → save as `custom-content.json` in this folder (replace the old one).
2. Run `python3 tools/sync_bundle.py`. It extracts the photos byte-exact into `photos/`, backs up your export in `original/`, and regenerates `custom-content.js`.
3. Upload the whole folder to your host.

## Phones (GitHub Pages)

1. Create a GitHub repo and upload the **contents** of this folder (so `index.html` is at the top level, with `photos/` next to it). Don't upload the ZIP itself.
2. Settings → Pages → Branch `main`, folder `/ (root)` → Save. Open the `https://<you>.github.io/<repo>/` link on the phone.
3. On the phone: tap **START**, then **turn the phone sideways** — the game fills the screen with a joystick (bottom-left) and a JUMP button (bottom-right). The ⤢ button goes fullscreen (Android Chrome). Portrait works too, just smaller.
4. Optional: Chrome menu → *Add to Home screen / Install app* for a fullscreen app icon (on iPhone: Share → Add to Home Screen).
Music starts after the first tap (phone browsers require that). The game auto-pauses if the tab is hidden.

## Controls

A/D or ←/→ move · Space/W/↑ jump (double jump) · Esc pause · mobile joystick + jump button.
