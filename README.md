# Nova Hub — Setup Guide

A parent app for your team: competition schedule with countdown, practice times and practice wear, events, a shared calendar, a packing list with pictures, contacts, FAQ, and a "suggest an update" form. The sample is a made-up team called **Nova**; swap in your own name, logo and colors. It installs on a phone's home screen like a regular app and works offline.

Everything you need to change lives in **one place**: the settings block at the top of `index.html`. You don't need to touch the rest of the file.

## What's in this folder

| File | What it is |
| --- | --- |
| `index.html` | The whole app, including all your settings at the top |
| `manifest.json` | The app's name and colors for the phone's home screen |
| `service-worker.js` | Lets the app work offline and pick up your updates |
| `icons/` | The home-screen icons (replace these with your own) |
| `images/` | Your logo and the pictures used in the app (practice wear, uniform, hair and makeup flat lays) |

## 1. Make it yours (about 15 minutes)

Open `index.html` in any text editor (Notepad, TextEdit in plain-text mode, VS Code, or GitHub's built-in editor). Near the top you'll find a big comment that says **NOVA HUB — SETTINGS**. Everything under it is clearly labeled, in this order:

1. **Basics** — team name, subtitle, logo, colors, page style, which tabs to show, quick links, office info
2. **Competitions** — the schedule, hotel booking dates, travel dates, ticket and schedule links
3. **Practice** — weekly practice cards, the "What to Wear" pictures, one-off announcements, closures
4. **Payments** — the "next payment" card on Home (leave the list empty to hide it)
5. **Latest updates** — the news feed on Home
6. **Events** — clinics, fundraisers, team events
7. **Student standouts**
8. **Contacts**
9. **FAQ**
10. **Photos**
11. **Comp packing list** — the checklist, with a picture above each group

The app ships with **sample data** so you can see how everything looks. Replace each sample with your real information and delete what you don't need. Dates use the format `"2026-11-15"`. The samples use a helper called `inDays(n)` (meaning "n days from today") so the demo always looks current; just replace those with real dates.

### Name and colors

- `teamName`, `headerSubtitle`, `gymName` — the header text and wording used in the app.
- `brandColor` — your main color (buttons, links, highlights). Use any hex color, like `"#e11d48"`. The app builds the lighter and darker shades itself. The sample uses emerald green.
- `darkColor` — the dark color behind the header, the bottom bar and the "Next Competition" card. The sample uses deep green.
- `pageStyle` — `"navy"` gives a dark background with white cards (the sample look). `"light"` gives a light background.
- `headerBanner` — a wide picture across the top of every page (the sample is `images/header-banner.jpg`, with the gym and team name on it). Replace the file with your own banner, or set it to `""` to use the `logoUrl` + text header instead. About 2.5 times wider than tall works well.
- `backgroundImage` — an optional picture behind the top of every page (the sample uses a green aurora sky, `images/aurora-bg.jpg`). Set it to `""` for a plain dark color. The logo in `images/nova-logo.png` is a transparent PNG, so it sits nicely on top.
- `logoUrl` — your logo, shown big at the top. Put the file in the `images` folder (a PNG with a transparent background that looks good on a dark color works best) and enter its path, like `"images/logo.png"`. Leave it blank to show the team name as text instead.
- `showHeader: false` swaps the header for a thin color strip.

### Turn tabs on or off

In `tabs: { ... }`, set any tab to `false` to hide it. Photos is off by default; turn it on after adding images to the `photos` list.

### The "Suggest Update" form

Create a free form in Jotform or Google Forms, copy its embed/share link, and paste it into `suggestFormUrl`. Parents then submit news from inside the app, and you add approved items to the **Latest updates** list. Until you add a link, the tab shows a sample form so you can see how it will look (it doesn't send anything). You can also hide the tab.

### Optional video

Put a video file next to `index.html` (for example `tutorial.mp4`) and set `tutorialVideo`. A button appears in Quick links. Leave it blank to hide the button.

### Pictures

The pictures live in the `images` folder. Replace a file with your own (keep the same name), or change the file names in the settings. Parents can tap any picture to enlarge it. To remove one, delete its line in the settings.

- Practice tab: the `practiceWear` list. Each picture has a `days` line (for example `days:["Monday"]`) that must match a day in your practice list. The app shows those days and times under the picture so parents can see which outfit goes with which practice.
- Packing list: the `imgs` line on each group in the `checklist` list. A picture can be limited to the Girls or Boys view with `for:"girls"` or `for:"boys"`. Items work the same way, so the Boys view shows only what a boy needs to pack.

## 2. Edit these three lines too

Near the very top of `index.html` there are three short lines to update so the app's name is right on the home screen:

- the `<title>` line
- the `apple-mobile-web-app-title` line
- `"name"` and `"short_name"` in `manifest.json`

## 3. Replace the icons

Replace the four PNG files in the `icons/` folder with your own artwork. (The sample uses a star.) Keep the file names and sizes the same:

- `apple-touch-icon.png` — 180 × 180
- `icon-192.png` — 192 × 192
- `icon-512.png` — 512 × 512
- `icon-512-maskable.png` — 512 × 512, with the artwork kept inside the center 70% so the phone's rounded-corner crop doesn't cut it off

Use a solid (non-transparent) square for best results on iPhone.

## 4. Put it online (free, with GitHub Pages)

1. Create a free account at github.com, then click **New repository**. Pick a name, for example `nova-hub` (any name works).
2. Click **uploading an existing file**, drag in everything from this folder (keep the `icons` and `images` folders), and commit.
3. Go to **Settings → Pages**. Under "Build and deployment", choose **Deploy from a branch**, pick **main** and **/ (root)**, then Save.
4. After a minute or two, the page shows your link: `https://YOUR-USERNAME.github.io/REPO-NAME/`. Open it on your phone to check.

Notes on GitHub Pages: on a free account the repository must be public for Pages to work, and the published link is open to anyone who has it. The app asks search engines not to list it (the `robots` line in the head), so it's unlikely to show up in Google, but treat the link as shareable. Don't put anything in the app you wouldn't be comfortable with anyone who has the link seeing. Other hosts, such as Netlify and Cloudflare Pages, also work. This is a plain static site with no server.

## 5. Share it with parents

Send the link in your team chat. On an iPhone, open it in Safari, tap **Share → Add to Home Screen**. On Android, open it in Chrome and tap **⋮ → Add to Home screen** (or **Install app**).

## 6. Keeping it up to date

Edit the settings block and save the file in GitHub (**pencil icon → Commit changes**). Parents see the change the next time they open the app. The app always checks for the newest version first and only uses its saved copy when there is no connection.

## Good to know

- Parents' own calendar events, packing-list checkmarks, and travel notes are saved **on their own phone only**. You never see them, and they don't sync between devices.
- Past events, expired updates, and passed closures hide themselves automatically.
- If two gyms share one hosting account, give each a different `storageKey` in the settings so saved data never mixes.
- Fonts load from Google Fonts. If a parent is offline the first time, the app falls back to a standard font.

## Troubleshooting

| Problem | Fix |
| --- | --- |
| Blank page after editing | A quote, comma, or bracket was probably deleted by accident. Undo your last change. Each item in a list is wrapped in `{ }` and separated by commas. |
| The link shows a 404 | Pages isn't turned on yet, or `index.html` isn't at the top level of the repository. Check Settings → Pages and wait a few minutes. |
| Old version still showing | Close the app completely and reopen it. If it still looks stale, change the version number in `service-worker.js` (`nova-hub-v1` to `nova-hub-v2`). |
| An icon didn't change on the home screen | Delete the app from the home screen and add it again. |
