# Key Engineering — Customer Ledger

A single-file, offline-first app for tracking customers and the materials used for their jobs.

## Running it

No build step, no server, no dependencies to install. Just open `customer-ledger.html` in any modern browser (Chrome, Safari, Edge, Firefox).

## Where your data lives

Data is saved to your browser's `localStorage`, scoped to **this file's origin**. That means:

- Data persists across reloads and browser restarts on the **same device and browser**.
- It does **not** automatically sync to other devices or browsers by default — there's no server involved.
- Opening the file from a different location (e.g. a different folder, or via `file://` vs a hosted URL) may count as a different origin and start with empty data.

## Syncing to OneDrive

In Chrome or Edge, click **☁ Connect OneDrive folder** and pick your local OneDrive-synced folder (e.g. `OneDrive\Key Engineering` or similar). From then on, every change you make is automatically written to a file called `key-engineering-customers.json` in that folder, and OneDrive's own sync picks it up and pushes it to your other devices/the cloud as usual.

Notes:

- This only works in **Chrome or Edge** — Safari and Firefox don't support the browser API this relies on (File System Access API), so the button won't appear as usable there.
- The browser remembers the folder you picked, so you shouldn't need to reconnect on every visit — but if it ever loses permission (e.g. after clearing site data), you'll see a **reconnect** prompt.
- This app doesn't read that file automatically on other devices — each device still keeps its own local copy in `localStorage`. To actually pull in data synced from another device, use **Import backup** and select the synced `key-engineering-customers.json` file from your OneDrive folder.
- Disconnecting the folder just stops future auto-writes — it doesn't delete anything already saved there.

## Moving data between devices

Use the **Export backup** / **Import backup** buttons in the app:

1. On the device with your data, click **Export backup** — downloads a `.json` file.
2. Copy that file to the other device (AirDrop, email, USB, cloud drive, whatever's easiest).
3. On the other device, open the app and click **Import backup**, then select the file.

This overwrites whatever is currently in the app on the importing device, so export from there first if it also has data you want to keep.

## Hosting it (optional)

If you want a stable URL instead of opening a local file each time:

- **GitHub Pages**: push `customer-ledger.html` to a repo, enable Pages in the repo settings, rename the file to `index.html` (or point Pages at it directly). You'll get a URL like `https://yourusername.github.io/reponame/`.
- Any static host works the same way (Netlify, Vercel, a plain web server) — it's just one HTML file.

Note: your data is still per-browser even when hosted. Two people (or two browsers) visiting the same URL will each have their own separate local data, not a shared one.

## Backing up regularly

Since there's no server, your data only exists in that browser's storage. It's a good habit to click **Export backup** occasionally and keep the file somewhere safe, in case you clear browser data or switch machines.
