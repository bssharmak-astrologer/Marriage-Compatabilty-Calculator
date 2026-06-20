# నక్షత్ర పొంతన లెక్కింపు — Nakshatra Porutham Calculator

A installable PWA (Progressive Web App) for Sri Manjeera Jyothishyalayam, Pithapuram —
calculates the 36-point Ashtakoota nakshatra compatibility score for a groom and bride,
based on the supplied vadhu-vara gana table.

## Folder structure

```
porutham-pwa/
├── index.html              # the app itself (data is embedded inline, no server-side code needed)
├── manifest.json           # PWA manifest (name, icons, colors, display mode)
├── sw.js                   # service worker — caches everything for offline use
├── .nojekyll                # tells GitHub Pages not to run Jekyll on this folder
└── icons/
    ├── icon-192.png
    ├── icon-512.png
    └── apple-touch-icon.png
```

Everything is static — there is no backend, database, or build step. Any static host works.

## Deploy to GitHub Pages (free)

1. **Create a new repository** on GitHub (e.g. `porutham-calculator`). Public repos get free Pages hosting.
2. **Upload all the files in this folder** to the repository, keeping the folder structure exactly
   as it is above (the `icons/` folder must stay a folder, not be flattened).
   - Easiest way: on the repo's GitHub page, click **Add file → Upload files**, then drag in
     `index.html`, `manifest.json`, `sw.js`, `.nojekyll`, and the `icons` folder together.
   - Or, if you use git on your computer:
     ```bash
     git init
     git add .
     git commit -m "Initial commit: Nakshatra Porutham Calculator"
     git branch -M main
     git remote add origin https://github.com/<your-username>/porutham-calculator.git
     git push -u origin main
     ```
3. **Turn on Pages**: in the repo, go to **Settings → Pages**. Under "Build and deployment",
   set **Source** to "Deploy from a branch", **Branch** to `main` and folder `/ (root)`. Save.
4. Wait about a minute, then your app is live at:
   ```
   https://<your-username>.github.io/porutham-calculator/
   ```
5. Open that link on your phone → browser menu → **Add to Home Screen** (Android) or
   **Share → Add to Home Screen** (iPhone). Because this is now served over HTTPS, it installs
   as a real app: its own icon, full-screen window, and it keeps working even with no internet
   after the first visit (the service worker caches everything).

## Updating the points table or branding later

- All the nakshatra/animal/ganam/nadi/points data lives in one JavaScript object near the top
  of `index.html` (search for `const DATA = `). Edit numbers there directly if a correction is
  ever needed — no other file needs to change.
- The letterhead (institution name, place, proprietor name) is plain HTML near the top of the
  `<body>` — search for `letterhead` in `index.html`.
- To change the app icon: replace the three PNG files in `icons/` (keep the same filenames and
  sizes — 192×192, 512×512, and 180×180 for `apple-touch-icon.png`), then bump `CACHE_NAME` in
  `sw.js` (e.g. `porutham-cache-v2`) so phones that already installed the app pick up the change.

## Notes

- The current app icon is a simple kalasha placeholder. Swap in your own logo or photo (one you
  hold the rights to) into `icons/` whenever you're ready — see above.
- This is a static lookup tool, not a substitute for a qualified astrologer's full reading.
