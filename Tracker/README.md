# Full-Stack Journey Tracker

A single-file, zero-backend progress tracker for a full-stack learning roadmap. Data lives in your browser and — once cloud sync is on — in a **private GitHub Gist**, so laptop, phone and work PC all see the same thing. Everything is free.

```
index.html   ← the whole app (HTML + CSS + JS)
README.md    ← this guide
```

---

## How the tracker works (2-minute version)

**Sessions are the unit.** Every roadmap task is a number of *sessions* — one sitting of about 2 hours. Course sections, readings and blog posts are one session; project steps are 2–8. Click a task to log a session (a one-session task just toggles), `–` undoes one, `+plan` says "this is taking longer than I estimated". A task is complete when logged ≥ planned.

**Declare the week on Sunday** from your real calendar, not your intentions:

| Mode | Plans | Use when |
|---|---|---|
| **DEFAULT** | 4 sessions (~8h) | A normal week: two weeknights + one weekend block. |
| **REDUCED** | 2 sessions (~4h) | Busy week. Keep the active track warm, fill fragments with certs/reading. |
| **FALLBACK** | 0 sessions | No capacity. One ≤30-min keep-warm touch so the thread doesn't snap. |

The mode is a **floor, not a ceiling**. Finished early? Press **Pull next →** to plan one more session from the roadmap, as many times as you like (it warns past 8/week). Every session you log counts, whether it was planned, pulled in, or logged from the Roadmap tab before you even declared.

**The week closes itself** at the end of the calendar week and records how many sessions you logged. Change mode mid-week if reality changed — nothing you logged is lost.

**Velocity is measured, not declared.** Each completed week scores `sessions logged ÷ DEFAULT budget` (4 sessions = 1.0, 6 = 1.5, 2 = 0.5). The projection averages the last 8 calendar weeks; weeks with nothing logged count as 0. So the two Projection dates (Soft Applications Open, Full Push) move earlier only when you actually do more — or when you cut scope. After four straight weeks well over or under budget, the app suggests adjusting DEFAULT (Data → Budgets).

**Two daily habits carry everything:** log the drill (pull → sync → quiz → answer live → commit) and bump the commit counter. Certs, system design and AI literacy are "passive" pools with unit counters in Threads; REDUCED and FALLBACK weeks pull one item from each, and ticking it logs one unit.

All budgets, hours-per-session, the soft cap and flag thresholds are editable in the Data tab.

---

## Can I keep it private?

- **Your data** is private either way. It never goes to the hosting provider — it lives in your browser and in a *secret* gist that only your token can write to.
- **The app file (`index.html`)** is private only if the repo is private. GitHub Pages on a free account requires a **public** repo, so:
  - Want the repo private → deploy with **Vercel** (free Hobby plan supports private repos). This is the recommended path below.
  - Don't mind the code being public (it contains no secrets or data) → GitHub Pages works too.

Nothing sensitive is ever in the file, so either is safe. The choice is purely whether other people can read the code.

> Note: GitHub "secret" gists are unlisted, not encrypted. Anyone with the exact gist URL could read it, but there is no way to discover it. Your token is required to *write*. This is fine for a learning tracker; don't put passwords or personal data in it.

---

## Step 1 — Create a GitHub token (once)

The app needs one token with permission to read/write gists. Nothing else.

1. GitHub → click your avatar → **Settings** → scroll to **Developer settings** (bottom of the left menu) → **Personal access tokens** → **Fine-grained tokens** → **Generate new token**.
2. Token name: `journey-tracker`. Expiration: pick the maximum (1 year — you'll re-paste it once a year; the app will tell you when it stops working).
3. **Repository access:** leave the default. The token needs no repos.
4. **Permissions → Account permissions → Gists → Read and write.** That's the only permission to add.
5. **Generate token** and copy it (`github_pat_…`). Keep it somewhere safe (a password manager). You'll paste it once into each device.

*Alternative:* a **classic** token with only the `gist` scope can be set to never expire. Slightly less tidy, but no yearly renewal.

---

## Step 2 — Put it on GitHub and deploy

### Option A — private repo + Vercel (recommended)

1. GitHub → **New repository** → name it `journey-tracker` → **Private** → Create.
2. Upload the files: on the empty repo page click **uploading an existing file**, drag in `index.html` and `README.md`, **Commit**.
   (Or with git: `git init`, `git add .`, `git commit -m "tracker"`, `git remote add origin …`, `git push -u origin main`.)
3. Go to [vercel.com](https://vercel.com) → **Sign up / Log in with GitHub** (free Hobby plan).
4. **Add New → Project** → **Import** `journey-tracker` (grant Vercel access to that repo when asked).
5. Framework preset: **Other**. Leave build settings empty. **Deploy.**
6. You get a URL like `https://journey-tracker-xxx.vercel.app`. Bookmark it on every device; on your phone use "Add to Home Screen" so it feels like an app.

Every future `git push` to `main` redeploys automatically. Custom domain later (e.g. `tracker.tjamaly.com`) is Project → Settings → Domains.

### Option B — public repo + GitHub Pages

1. Create the repo as above but **Public**, upload the files.
2. Repo → **Settings** → **Pages** → Source: **Deploy from a branch** → Branch `main`, folder `/ (root)` → **Save**.
3. After a minute your site is at `https://<your-username>.github.io/journey-tracker/`.

---

## Step 3 — First device: connect and create the gist

1. Open the deployed URL. Go to the **Data** tab → **Cloud sync** panel.
2. Paste your token into the token box.
3. Leave the gist id **empty** and click **Create new gist**. The app creates a private gist named `journey.json` containing your current data and shows you the **gist id**. Copy it (it's also filled into the box, and saved in this browser).
4. The pill under your name in the header now reads **synced**.

If you already had data in this browser (from using the file locally), that data is what gets uploaded — nothing is lost.

## Step 4 — Every other device

1. Open the same URL → **Data** tab → Cloud sync.
2. Paste the **same token** and the **gist id** from Step 3 → **Save & sync now**.
3. It pulls the cloud copy and the pill turns **synced**. Done — you only ever do this once per device (plus once a year when the token expires).

---

## How sync behaves (so nothing surprises you)

- **Local first.** Every tick is saved to the browser instantly. About 1.5 s later it's pushed to the gist. Offline, it just keeps working locally and catches up next time it can.
- **Pull on open, and whenever you come back to the tab** (phone → laptop works naturally). The newer copy wins by timestamp.
- **Never pushes blind.** A device always pulls first in a session, so a stale device can't silently overwrite newer data.
- **Last write wins — per file.** If you edit on two devices while one is offline, whichever *saved most recently* wins as a whole. Practical rule: **use one device at a time**, and let the pill say "synced" before switching. If it ever bites, every push is a gist revision — open `https://gist.github.com/<you>/<gist-id>/revisions` to recover an older copy.
- **Reset to seed** also overwrites the cloud copy (it warns you).
- **Export JSON** is still your offline backup and never contains the token.
- The token and gist id are stored only in that device's browser (`localStorage`), not in the app file, not in exports, not in the gist.

Header pill states: `synced · 2m ago` · `unsynced changes…` · `syncing…` · `offline / sync failed — will retry` · `token rejected — check Data tab` · `sync off · local only`.

---

## Updating the app later

Edit `index.html`, commit, push. Vercel/Pages redeploys. Your data is unaffected (it's in the browser + gist, not the file). When a version changes the data shape, the built-in `migrate()` upgrades old data in place — v7 (session-based tasks) migrates older tick-based data automatically: ticked tasks become fully-logged sessions, past weeks get an estimated session count, and the current week is re-declared.

Replacing an already-deployed v6 with v7: just push the new file. The first device to open it upgrades its local copy and pushes; other devices pull the upgraded copy (newer timestamp wins). **Do a hard refresh on every device right after deploying** (a browser tab still running the old version would read the new data through old code). Newer-version data is refused by older code rather than mangled, but refreshing first avoids the confusion entirely.

---

## Troubleshooting

| Symptom | Fix |
|---|---|
| Pill says **token rejected** | Token expired or lacks the Gists **Read and write** permission. Make a new one (Step 1) and paste it on each device. |
| Pill says **gist not found** | Wrong id, or the gist was deleted. Copy the id from the first device (Data tab) or from `gist.github.com`. |
| **offline / sync failed** while online | Corporate firewall blocking `api.github.com`, or a GitHub hiccup. It retries on the next change and when you return to the tab. |
| Two devices disagree | Check both are on the same gist id. Refresh the older one — pull wins if the cloud is newer. Otherwise use gist **Revisions** to recover. |
| Data tab shows a red **"could not be loaded"** banner | Local storage got corrupted. Nothing is overwritten. Use **Pull from cloud** to restore from the gist, or **Download stored data** to inspect it. |
| Token leaked | GitHub → Settings → Developer settings → revoke it. Create a new one. Nobody can read the gist history without the URL, but revoke anyway. |

---

## Local development

Just open `index.html` in a browser — no build step. Local `file://` data is separate from the deployed site's data (different origin); set up sync on both, or export/import.
