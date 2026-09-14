# Key Engineering — Customer Ledger

A single-file, offline-first app for tracking customers and the materials used for their jobs.

## Running it

No build step, no server, no dependencies to install. Just open `customer-ledger.html` in any modern browser (Chrome, Safari, Edge, Firefox).

## Rope measuring tool

Click **+ Add rope** (top of the app, or inside a customer's expanded card) to log a crane rope calculation against a customer: location, crane number, rope size, crane details, SWL, number of falls, and drum reeve details (number / length / extra rope). Load per fall and total rope required are calculated automatically, the same way as the original spreadsheet. Saved entries show up under that customer's "ropes" list.

## Editing entries

Every material and rope entry has an **edit** button next to **remove**. It reopens the same form pre-filled with the current values — rope totals recalculate automatically when you save changes.

## Photos

Both the material and rope forms have a **📷 Add / upload photo** button. Photos are compressed and stored alongside the entry, and show as a small thumbnail in the list — tap it to view full-size. Since photos are stored as part of your local data, a lot of high-resolution photos can add up; the app compresses each one on upload to keep this manageable, but it's still worth exporting backups regularly (see below).

## Search

The search bar at the top finds customers by name or company, and also by material name or rope details (location, crane number, rope size) — so you can look up a part and find which customer it belongs to.

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
- This app doesn't read that file automatically on other devices — each device still keeps its own local copy in `localStorage`. To actually pull in data synced from another device, use **Merge in backup** and select the synced `key-engineering-customers.json` file from your OneDrive folder. This merges rather than overwrites, so it's safe to do even if the device already has its own entries.
- Disconnecting the folder just stops future auto-writes — it doesn't delete anything already saved there.

## Moving data between devices / working as a team

Use **Export backup** / **Merge in backup** to combine everyone's work:

1. Each person exports their own data (**Export backup**) into your shared OneDrive folder — give the file a distinct name per person if you're doing this regularly (e.g. `customers-dave.json`).
2. On the device that should end up with everything, use **Merge in backup** for each person's file, one at a time.
3. Importing now **merges** rather than replacing — it adds any customers, materials, or ropes it doesn't already have, and shows a summary of what came in (e.g. "Merged in: 2 new customers, 5 new materials"). If the same entry was edited in two places, it keeps whichever edit is more recent.
4. Once a device has the full merged set, export from there and have everyone else **Merge in backup** that file, so all devices end up in sync.

**Important limitation:** this is a manual, merge-on-import process, not live sync — two people entering data at the same time on different devices won't see each other's changes until someone exports and everyone else imports. It also can't sync *deletions*: if someone deletes an entry on their device, merging their old export elsewhere won't remove it there too (merging only ever adds or updates, never deletes), so deleting a customer or entry is best done consistently across devices as a manual step, or by re-exporting and re-merging afterwards.

If you outgrow this — e.g. several people need to see each other's entries appear automatically, in real time — that needs a proper shared backend (like Supabase) instead of file-based merging. That's a bigger change than this app currently has, but it's doable if this manual merge workflow becomes a hassle.

## Hosting it (optional)

If you want a stable URL instead of opening a local file each time:

- **GitHub Pages**: push `customer-ledger.html` to a repo, enable Pages in the repo settings, rename the file to `index.html` (or point Pages at it directly). You'll get a URL like `https://yourusername.github.io/reponame/`.
- Any static host works the same way (Netlify, Vercel, a plain web server) — it's just one HTML file.

Note: your data is still per-browser even when hosted. Two people (or two browsers) visiting the same URL will each have their own separate local data, not a shared one.

## Backing up regularly

Since there's no server, your data only exists in that browser's storage. It's a good habit to click **Export backup** occasionally and keep the file somewhere safe, in case you clear browser data or switch machines.
