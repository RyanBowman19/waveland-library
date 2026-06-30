# The easy way — just copy & paste these files

Everything in this folder is **ready to paste straight into WordPress**. The colors,
fonts, and photos all load automatically from the live GitHub site, so there is
**no CSS to paste and no images to upload.** You only ever copy a file and paste it.

The same move every time: **open the file → Ctrl+A (select all) → Ctrl+C (copy) →
in WordPress add a "Custom HTML" block → Ctrl+V (paste) → Save/Publish.**

---

## Do these in order

### 1. Turn on a block theme (one time)
In WordPress: **Appearance → Themes → Add New** → search **Twenty Twenty-Four** →
**Install** → **Activate**. (You need this so "Appearance → Editor" exists.)

### 2. Paste the Header (one time)
- **Appearance → Editor → Patterns → Template Parts → Header.** Delete anything there.
- Add a **Custom HTML** block.
- Paste the whole contents of **`_HEADER.html`**. Save.

*(This header file is also the thing that loads the site's styling, so do it before
looking at any page — otherwise pages look like plain text until it's in.)*

### 3. Paste the Footer (one time)
- **Appearance → Editor → Patterns → Template Parts → Footer.** Delete anything there.
- Add a **Custom HTML** block.
- Paste the whole contents of **`_FOOTER.html`**. Save.

### 4. Make the 8 pages (one paste each)
For each row below: **Pages → Add New Page**, type the **Title**, add **one Custom HTML
block**, paste the whole matching file, then **Publish**.

| Page Title (type this exactly) | Paste this file | Make sure the page's URL is |
|---|---|---|
| Home | `home.html` | `/` (set in Step 5) |
| About & History | `about.html` | `/about/` |
| Services | `services.html` | `/services/` |
| Research | `research.html` | `/research/` |
| Policies | `policies.html` | `/policies/` |
| Contact | `contact.html` | `/contact/` |
| Events | `events.html` | `/events/` |

> When you type the title, WordPress shows the page's web address ("Permalink") under it.
> It should match the right column (e.g. the About page should be `/about/`). If it's
> different, click **Edit** next to the permalink and fix it — otherwise the menu links
> won't line up.

### 5. Set the Home page as the front page (one time)
**Settings → Reading → "Your homepage displays" → A static page → Homepage: Home.** Save.

That's the whole site. Visit it and click around the menu.

---

## If something looks off
- **Plain text, no colors/photos** → the Header (Step 2) didn't save, or it's missing the
  top lines of `_HEADER.html` (the `<link ...>` lines). Re-paste the *entire* file.
- **A menu link says "page not found"** → that page's URL doesn't match the table in Step 4.
  Fix the page's permalink.

## Good to know
- The styling and photos are served from the live GitHub site
  (`ryanbowman19.github.io/waveland-library`). Keep that GitHub repo published and the
  WordPress site will keep looking right. If you ever want everything self-contained inside
  WordPress instead, ask and I'll switch it over.
- This is the "just get it live" version. If you later want staff to edit Hours or Events
  without touching code, that can be added — ask anytime.
