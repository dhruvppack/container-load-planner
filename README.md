# Container Load Planner

Plan an export container load before it happens: choose the container, enter the cargo, and get

- four loading options to compare (Heavy first, Maximum fill, Your list order, Balanced weight)
- units that fit and units left over, with the reason
- volume, payload, free space in cbm, and how much more you can fill
- front/door and left/right weight balance, with warnings
- a 3D load plan you can step through, plus top and side drawings
- step-by-step loading instructions with pictures
- PDF export, copyable summary, and plan files you can move between devices
- a pallet loading planner: boxes per layer and per pallet, column or interlocked layers, load height and weight, pallets needed for a shipment, 3D pallet view and PDF export (EUR, block, US, half EUR or custom pallets)

Containers: 20' GP, 40' GP, 40' HC, 45' HC and custom sizes. Metric by default, imperial optional.

The whole app is one page (`index.html`) with no build step. It runs in any modern browser and can be installed as an app on iPad, iPhone, Android, Windows and Mac.

## Files

| File | What it does |
| --- | --- |
| `index.html` | The app: layout, packing engine, 3D view, exports |
| `manifest.webmanifest` | App name, icon and colours used when installed |
| `sw.js` | Offline support: caches the app, libraries and fonts |
| `icons/` | App icons for home screens and the desktop |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

Libraries are loaded from cdnjs/jsDelivr at pinned versions: three.js r128 (3D view) and jsPDF 2.5.1 (PDF export). After the first online start they are cached, so the app also works offline.

## Hosting

The app must be served over **https** to be installable and to work offline.

**GitHub Pages** (Settings → Pages → Build and deployment → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)` → Save).
The app is then at `https://dhruvppack.github.io/container-load-planner/`.
For a **private** repository GitHub Pages needs a paid GitHub plan (Pro, Team or Enterprise). The published site itself is public unless your organisation restricts it.

**Free alternatives that work with a private repository:** Cloudflare Pages or Netlify. Connect the repository, leave the build command empty, set the output folder to `/` (root). Every push to `main` updates the app.

## Install as an app

**iPad / iPhone (Safari)**
1. Open the app address in Safari.
2. Tap **Share** → **Add to Home Screen** → **Add**.
3. Start it from the home screen icon. It opens full screen like a normal app.

**Windows or Mac (Chrome or Edge)**
1. Open the app address.
2. Click the **install icon** at the right end of the address bar (or menu → *Install Container Load Planner*).
3. It gets its own window, a Start menu / Dock icon, and can be pinned to the taskbar.

**Mac (Safari 17 or newer)**: File → **Add to Dock**.

Open the app once while online after installing, so the 3D and PDF libraries are cached for offline use.

## Your data

Plans and the current draft are saved in the browser storage of each device. They are not uploaded anywhere.
To move a plan to another device, use **Export plan file** and then **Import plan file** on the other device.
Removing the app or clearing website data deletes the saved plans on that device.

## Updating

Change `index.html`, commit and push to `main`. Installed apps pick up the new version the next time they are opened online.
If you change `sw.js` or the icons, also raise `VERSION` at the top of `sw.js` (for example `clp-v2`) so old caches are cleared.

## Run locally

```
python3 -m http.server 8080
```
Then open `http://localhost:8080`.

## Notes

Loading plans are planning estimates. Always check gross weights, the payload on the container's CSC plate and road weight limits, and secure any free space before sealing.
