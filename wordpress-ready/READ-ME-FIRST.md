# The easy way — copy & paste these files

Everything here is **self-contained**: the styling is built into the Header file, and the
photos get uploaded into the library's own WordPress. **Nothing depends on any outside
website** — once it's in, it's 100% the library's.

The same move every time: **open a file → Ctrl+A (select all) → Ctrl+C → in WordPress add a
"Custom HTML" block → Ctrl+V → Save/Publish.**

There are only two kinds of edit you ever make, and both are find-and-replace:
- Wherever you see **`PASTE_..._URL`**, swap in a photo address (Step 2 explains).
- Nothing else — links are already done.

---

## Step 1 — Turn on a block theme (one time)
**Appearance → Themes → Add New** → search **Twenty Twenty-Four** → **Install** → **Activate**.
(You need this so "Appearance → Editor" exists.)

## Step 2 — Upload the 5 photos and copy their addresses
**Media → Add New Media File**, then drag in these 5 files from the project's `images` folder.
After each uploads, click it and copy its **"File URL."** Paste them into a blank note so you
have them ready:

| Photo file | When you see this placeholder… | …paste this photo's URL |
|---|---|---|
| `library-logo.jpg` | `PASTE_LOGO_URL` | |
| `library-exterior.jpg` | `PASTE_EXTERIOR_PHOTO_URL` | |
| `library-exterior-sketch.jpg` | `PASTE_SKETCH_PHOTO_URL` | |
| `andrew_carnegie.jpg` | `PASTE_CARNEGIE_PHOTO_URL` | |
| `LibraryPassportLogo-removebg-preview.png` | `PASTE_PASSPORT_LOGO_URL` | |

## Step 3 — Paste the Header (one time)
- **Appearance → Editor → Patterns → Template Parts → Header.** Delete anything there.
- Add a **Custom HTML** block, paste all of **`_HEADER.html`**.
- Find **`PASTE_LOGO_URL`** in what you pasted and replace it with the `library-logo.jpg` address.
- **Save.**

*(The Header file also contains the site's entire styling, so do it before viewing any page —
until it's saved, pages will look like plain text. That's normal.)*

## Step 4 — Paste the Footer (one time)
- **Appearance → Editor → Patterns → Template Parts → Footer.** Delete anything there.
- Add a **Custom HTML** block, paste all of **`_FOOTER.html`**. (No placeholders here.) **Save.**

## Step 5 — Make the 8 pages (one paste each)
For each row: **Pages → Add New Page**, type the **Title**, add **one Custom HTML block**, paste
the whole matching file, replace any **`PASTE_..._URL`** placeholders, then **Publish.**

| Page Title (type exactly) | Paste this file | Placeholders to replace | Page address should be |
|---|---|---|---|
| Home | `home.html` | `PASTE_EXTERIOR_PHOTO_URL` | `/` (set in Step 6) |
| About & History | `about.html` | `PASTE_EXTERIOR_PHOTO_URL`, `PASTE_SKETCH_PHOTO_URL`, `PASTE_CARNEGIE_PHOTO_URL` | `/about/` |
| Services | `services.html` | `PASTE_PASSPORT_LOGO_URL` | `/services/` |
| Research | `research.html` | none | `/research/` |
| Policies | `policies.html` | none | `/policies/` |
| Contact | `contact.html` | none | `/contact/` |
| Events | `events.html` | none | `/events/` |

> When you type the title, WordPress shows the page's web address ("Permalink") under it. It
> should match the last column (e.g. About should be `/about/`). If it's different, click
> **Edit** by the permalink and fix it, or the menu links won't connect.

## Step 6 — Set Home as the front page (one time)
**Settings → Reading → "Your homepage displays" → A static page → Homepage: Home.** Save.

Done — visit the site and click through the menu.

---

## If something looks off
- **Plain text, no colors/photos** → the Header (Step 3) didn't save, or you didn't paste the
  *whole* `_HEADER.html` (it must start with the `<link ...>` and `<style>` lines). Re-paste it all.
- **A photo is a broken-image icon** → a `PASTE_..._URL` was missed, or the URL was pasted wrong.
- **A menu link says "page not found"** → that page's address doesn't match the table in Step 5.
  Fix the page's permalink.

## Notes
- The Header file already includes fixes for Twenty Twenty-Four's default behavior (it hides the
  automatic page title WordPress adds, and lets the hero run full width instead of being boxed in).
  So you do **not** need to touch "Additional CSS" — just make sure you pasted the whole
  `_HEADER.html`. If you already pasted an older copy of the Header, re-paste this updated one.
- The fonts load from Google Fonts (standard and free — not tied to anyone's account). Everything
  else lives inside the library's WordPress.
- This is the "just get it live" version. If you later want staff to edit Hours or Events without
  touching code, that can be added — ask anytime.
- That Andrew Carnegie photo originally came from Getty Images. Before going fully public, confirm
  it's okay to use, or swap in a free public-domain portrait of Carnegie (old photos of him are
  free to use). Just ask and I'll find one.
