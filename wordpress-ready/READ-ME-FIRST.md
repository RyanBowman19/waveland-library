# The easy way — copy & paste these files

Everything here is **self-contained**: the styling is built into the Header file, and the
photos get uploaded into the library's own WordPress. **Nothing depends on any outside
website** — once it's in, it's 100% the library's.

The same move every time: **open a file → Ctrl+A (select all) → Ctrl+C → in WordPress add a
"Custom HTML" block → Ctrl+V → Save/Publish.**

**The photos are already uploaded and their addresses are already baked into these files**, so
there is **nothing to edit** — just paste each file and publish. (Every image points at the
library's own Media Library at `waveland.lib.in.us/wp-content/uploads/`.)

---

## Step 1 — Turn on a block theme (one time)
**Appearance → Themes → Add New** → search **Twenty Twenty-Four** → **Install** → **Activate**.
(You need this so "Appearance → Editor" exists.)

## Step 2 — (already done) Photos are uploaded
The 5 photos are already in the Media Library and their web addresses are already written into
the files below, so you can skip straight to pasting. For reference, the photos in use are:
`library-logo.jpg`, `library-exterior.jpg`, `library-exterior-sketch.jpg`,
`andrew-carnegie-gettyimages-640453979.avif`, and `LibraryPassportLogo-removebg-preview.png`.

## Step 3 — Paste the Header (one time)
- **Appearance → Editor → Patterns → Template Parts → Header.** Delete anything there.
- Add a **Custom HTML** block, paste all of **`_HEADER.html`**.
- **Save.** (The logo address is already in the file — nothing to change.)

*(The Header file also contains the site's entire styling, so do it before viewing any page —
until it's saved, pages will look like plain text. That's normal.)*

## Step 4 — Paste the Footer (one time)
- **Appearance → Editor → Patterns → Template Parts → Footer.** Delete anything there.
- Add a **Custom HTML** block, paste all of **`_FOOTER.html`**. (No placeholders here.) **Save.**

## Step 5 — Make the 8 pages (one paste each)
For each row: **Pages → Add New Page**, type the **Title**, add **one Custom HTML block**, paste
the whole matching file, then **Publish.** (No edits needed — photos and links are already set.)

| Page Title (type exactly) | Paste this file | Page address should be |
|---|---|---|
| Home | `home.html` | `/` (set in Step 6) |
| About & History | `about.html` | `/about/` |
| Services | `services.html` | `/services/` |
| Research | `research.html` | `/research/` |
| Policies | `policies.html` | `/policies/` |
| Contact | `contact.html` | `/contact/` |
| Events | `events.html` | `/events/` |

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
- **A photo is a broken-image icon** → that photo isn't in the Media Library at the expected
  address (`waveland.lib.in.us/wp-content/uploads/2026/06/...`). Re-upload it with the same file name.
- **A menu link says "page not found"** → that page's address doesn't match the table in Step 5.
  Fix the page's permalink.

## Where the CSS lives
Two ways to load the styling — pick **one**, not both (so the CSS isn't duplicated):

- **All-in-one (simplest):** paste **`_HEADER.html`** into Template Parts → Header. Its styling is
  built in, so there's nothing else to do for CSS.
- **Separate CSS (what you're using):** paste **`_ADDITIONAL-CSS.css`** into **Appearance → Editor
  → Styles → ⋮ → Additional CSS** (this is built into WordPress — no plugin, nothing to install).
  If you go this route, your Header block should be the header markup only, without a `<style>`
  block, so the CSS isn't loaded twice.

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
