# Cupidate · Product Showcase

A one-page showcase of **Cupidate** (a proximity-first dating app) for my resume: what the app does,
demo videos for Android and iPhone, the engineering behind it, and download links.

**Live link:** _add after deploying_

---

## Read this first

Unlike the other showcases, this page was written **from the source code**, not from a context
document. Every claim on it was checked against the three repositories before it was written, so
there is no "confirm this before you share" table. Two things are still worth knowing:

| Item | Status |
|---|---|
| Product name | The page says **Cupidate**. The repos, the package names (`HintApp`, `dating-app-backend`, `dating-admin-panel`) and the mobile storage key (`hint_auth`) all still say **Hint**. Nothing on the page depends on that, but decide whether Cupidate is a rename before you point anyone at the code |
| `assets/logo.svg` | **Placeholder** — my own mark, drawn from the app's design tokens. Replace it with the official asset |

**Nothing on this page claims a user count, a match count or revenue.** The four figures in the dark
band are all structural — things you can point at in the repo:

| Figure | Where it comes from |
|---|---|
| 84 REST endpoints | router verbs across `routes/*.js` (45 index · 20 admin · 12 auth · 4 ai · 3 interests) |
| 12 data models | `mongoose.model()` exports across `models/` |
| 5 role levels | the `role` enum on the User schema |
| 4 AI features | the four routes in `routes/ai.js` |

If you add numbers of your own, make sure you can source them the same way.

---

## What's on the page

| Section | What it shows |
|---|---|
| Hero | Title, one-line pitch, your name and role, buttons, and the app screenshot |
| Demo | Android and iPhone screen recordings in phone frames |
| Scope | Four structural figures in a dark band, from `CONFIG.scope` |
| Features | Six feature cards — nearby discovery, signals, bottles, anonymous chat, messaging, AI helper |
| What I built | Six engineering highlights and an architecture diagram |
| Tech | The stack, grouped into Mobile, Admin panel, Backend and Integrations |
| Collabs | Instagram reels, if you add any |
| Code | GitHub repositories (all three are marked private) |
| Download | App Store / Google Play / website buttons |

Plain HTML, CSS and JavaScript in one file, no build step. The only outside resources are Google
Fonts and Instagram's embed script, which loads only if there are reels to show.

---

## Folder structure

```
showcase/
├── index.html            # the whole page: HTML, CSS and JS
├── README.md
├── .gitignore
└── assets/
    ├── logo.svg          # PLACEHOLDER — replace with the real logo (see below)
    ├── images/
    │   └── hero.png      # you add this
    └── videos/
        ├── android.mp4   # you add this
        └── ios.mp4       # you add this
```

---

## The logo is a placeholder

`assets/logo.svg` is a mark I drew for this page: a gradient heart (the dating half of the product)
with two signal arcs (the nearby/radar half). **Replace it with the official asset.**

It's used in four places: the nav, the footer, the browser tab icon, and the phone placeholders.
Unlike the Noida Farms logo, this one is a **transparent SVG carrying its own gradient**, so it
renders correctly on the dark footer with no white plate and no `invert()` filter. If you swap in a
logo with a solid or white artboard, you'll need to add a background plate to `.foot .brand img`
and `.screen-ph img` — check the footer before you ship.

If you replace it with a `.png`, update the three `assets/logo.svg` references in `index.html` plus
the two `<link rel="icon">` tags.

---

## Colours and type

Taken straight from the app's design tokens in `src/utils/theme.js`:

```
neon #FF3DA6 · pink #FF85C8 · pinkLight #FFD6EC · violet #C847FF
bg #FDF5F8 · surface #FFFFFF · surfaceRaised #F7EEF3
text #1A0A12 · textSecondary #7A5568 · textGhost #C4A8B8
```

**One rule worth keeping:** `#FF3DA6` is only 3.25:1 against white, which fails accessibility
contrast for text. On this page it is used as a *fill* — icons, glows, gradients, the numbers on the
dark band — and never as text. `#B3006B` is 6.7:1 and carries every pink label, link and button.
If you restyle, keep that split.

The fonts are the app's own: **Playfair Display** (the app's `display` token is
`PlayfairDisplay-BoldItalic`, which is why every heading here is bold italic), **Plus Jakarta Sans**
for body text and **Instrument Sans** for UI labels — the same three families, loaded from Google
Fonts. The hero deliberately splits the wordmark **Cupi**|**date**, ink then brand gradient.

---

## Preview locally

Serve the folder over HTTP. Opening the file directly mostly works, but Instagram embeds need a server.

```bash
cd ~/Desktop/Cupidate/showcase && python3 -m http.server 4321
```

Then open <http://localhost:4321>.

**On localhost, empty sections show placeholders** that say what's missing (for example "Add your
hero image at assets/images/hero.png"). **Once deployed, empty sections hide themselves**, so
visitors never see a half-finished page. That applies to Collabs, Code, Scope, any empty Tech card,
and the whole Download section if no store links are set.

---

## Editing: everything is in `CONFIG`

Open `index.html` and find `const CONFIG = {` near the bottom. You shouldn't need to touch the HTML or CSS.

| Field | What it does |
|---|---|
| `name`, `role` | Shown in the hero, footer and browser tab |
| `contact.email` / `linkedin` / `github` | Icon links in the hero and text links in the footer. Leave a field empty to hide it |
| `website`, `playStore`, `appStore` | **Currently blank.** Every store button, demo-section link and footer link reads from these |
| `hero` | Hero image. `framed: true` wraps a plain screenshot in a phone frame; `framed: false` if the image already contains the phone (use a transparent PNG) |
| `videos.android` / `videos.ios` | `src` (path or URL to an .mp4) and an optional `poster` image |
| `scope` | The four figures in the dark band |
| `tech` | The stack chips, grouped. An empty group hides itself once deployed |
| `instagram` | List of reels, each `{ url, label }`. Must be public to embed |
| `github` | List of repos. Set a `url`, or `private: true` for "Private repo · walkthrough on request" |

### Store links

All three are blank right now, so the page shows dashed "Coming soon" buttons on localhost and
hides the Download section entirely once deployed. Paste the URLs in and everything lights up at
once — the hero website button, the Android/iPhone links under the demos, the footer and the
download buttons all read from the same three fields.

---

## Hero image

`CONFIG.hero.src` points at `assets/images/hero.png`, which doesn't exist yet — so the hero shows a
placeholder phone. Add a real screenshot (about 9:19.5, like 1179×2556) and leave `framed: true`.

**Don't show real users' names, photos or locations** in a screenshot on a public page. This is a
dating app — use a demo account with obviously fake profiles.

<details>
<summary>Prompt for generating a hero mockup instead</summary>

```text
Create a high-quality product mockup image for a mobile app called "Cupidate", a proximity-first
dating app where you discover people nearby and send them a "signal".

CANVAS: portrait 1024×1536, fully TRANSPARENT background (PNG). No scene, no floor, no cast shadow.

DEVICE: one modern iPhone with thin black bezels and a Dynamic Island, centered, filling about 85%
of the canvas height, turned slightly (about 10°) for a subtle 3D angle. Realistic glass, no hands.

SCREEN: the Cupidate home screen in light mode. It must look like a real, polished app screenshot.
Screen background is a very pale pink (#FDF5F8) with white cards, 20px rounded corners and soft
pink-tinted shadows. Accent colour is hot pink (#FF3DA6) with violet (#C847FF) in gradients.
Headings use a bold italic serif; body text uses a clean geometric sans-serif. All text must be
sharp, correctly spelled, and exactly as written in quotes, with no other text anywhere.

Top to bottom:
1. iOS status bar showing "9:41".
2. Header: a small pink heart logo, then the word "Cupidate" in bold italic serif; a bell icon right.
3. A circular radar visual, pink concentric rings on white, with 4 small round profile photos
   scattered at different distances from the centre, and a label under it "12 people nearby".
4. Section title "Signals" with two side-by-side cards, each a profile photo with a name and a
   distance: "Aanya · 1.2 km" and "Meera · 3.4 km", each with a small pink heart button.
5. Section title "From the Void" with one wide card containing the text "anyone else awake?" and a
   small grey caption "2 hours ago · 6 replies".
6. Bottom tab bar with line icons and labels "Home" (active, pink), "Nearby", "Void", "Chats".

STYLE: warm, modern and playful but premium, like a top-rated App Store screenshot. Lots of white
space, crisp edges, soft pink glow.

AVOID: garbled or extra text, watermarks, hands, more than one phone, dark mode, clutter,
suggestive imagery, and any real person's likeness — use clearly generic illustrated avatars.
```

If the text comes out garbled, ask a follow-up: *"Keep everything exactly the same, only fix the
text so it reads: …"*

</details>

---

## Demo videos

Put recordings at `assets/videos/android.mp4` and `assets/videos/ios.mp4`, or point
`CONFIG.videos.*.src` at any hosted .mp4.

- **Orientation is detected automatically** — portrait gets a phone frame, landscape a wide frame.
- **Playback:** muted and looping while on screen, paused when scrolled away. The expand button goes
  full screen **with sound**.
- **If a file is missing**, the frame shows a placeholder, so the layout never breaks.

Again: record with a demo account. A screen recording of a dating app will otherwise show real
people's faces, names and distances.

Shrink a screen recording to a web-friendly size:

```bash
ffmpeg -i recording.mov -vf "scale=-2:1280" -c:v libx264 -crf 26 -preset slow -movflags +faststart -an android.mp4
```

`-an` removes audio. Aim for **under ~10 MB per video**; GitHub rejects files over 100 MB.

---

## Deploy

Any static host works.

**GitHub Pages:**

```bash
cd ~/Desktop/Cupidate/showcase && git init && git add . && git commit -m "Cupidate showcase"
```

Then add a remote, push, and set **Settings → Pages → Deploy from a branch → `main` / root**.

**Netlify Drop:** drag the `showcase` folder onto <https://app.netlify.com/drop>.
**Vercel:** run `npx vercel --prod` inside this folder.

`.gitignore` already contains `.DS_Store`.

---

## Accessibility

The page respects "reduce motion" (no autoplay, count-ups or reveal animations), works with the
keyboard, and every colour pairing meets WCAG AA. Verified responsive down to 375px with no
horizontal scroll.

---

## Before sharing: checklist

- [ ] Replace `assets/logo.svg` with the official logo (and check the dark footer still looks right)
- [ ] Decide the Cupidate / Hint naming question
- [ ] `name`, `role` and contact links are correct
- [ ] Hero screenshot added at `assets/images/hero.png` — **demo account only, no real profiles**
- [ ] `android.mp4` and `ios.mp4` added and compressed — **demo account only**
- [ ] Store links added, or Download section intentionally left hidden
- [ ] GitHub repos linked, or left as `private: true`
- [ ] Deployed and tested on a phone
- [ ] Link added to the resume
