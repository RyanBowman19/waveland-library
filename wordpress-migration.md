# Putting this site into WordPress — simple version

**The whole job is just three kinds of copy-paste:**

1. **The header** — paste once. Shows up on every page automatically.
2. **The footer** — paste once. Shows up on every page automatically.
3. **Each page's content** — one paste per page. Eight pages = eight pastes.

That's it. Every page works the exact same way: make the page, add **one** "Custom HTML" block, paste the content, fix the links/images, publish. No splitting things across multiple blocks.

Do the steps in order. Don't skip Steps 1–4 — the design won't look right until the CSS and header/footer are in.

---

## Step 1 — Turn on a block theme

In WordPress admin (the dashboard), go to **Appearance → Themes → Add New Theme**. Search for **Twenty Twenty-Four**, click **Install**, then **Activate**.

Now look at the left menu for **Appearance → Editor**. If you see "Editor," you're good. (If you only see "Customize" and no "Editor," the theme isn't the right kind — install **Twenty Twenty-Four** specifically, it definitely works.)

## Step 2 — Paste the styling (the CSS)

This is what makes everything look like the real site — the brick-red colors, the cards, the fonts. Without it, pages look like plain text. You only do this once.

1. Go to **Appearance → Editor**.
2. Click **Styles** (the half-circle/paintbrush icon), then the three dots **⋮ → Additional CSS**. (On some setups it's **Appearance → Customize → Additional CSS** instead — either is fine.)
3. First paste this line:

```css
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Source+Sans+3:wght@400;600;700&display=swap');
```

4. Then open the file **`css/style.css`** from this project, **select all of it** (Ctrl+A), copy, and paste it right below that line.
5. Click **Save**.

## Step 3 — Upload the photos

The site uses 6 image files. Upload them so WordPress has its own copy, then you'll grab a web address (URL) for each.

1. Go to **Media → Add New Media File**.
2. Drag in these files from the project's `images` folder:
   - `library-logo.jpg`
   - `library-exterior.jpg`
   - `library-exterior-sketch.jpg`
   - `andrew_carnegie.jpg`
   - `LibraryPassportLogo-removebg-preview.png`
3. After each one uploads, click it and copy the **"File URL"** (looks like `https://yoursite.org/wp-content/uploads/2026/06/library-logo.jpg`).
4. **Keep these URLs handy** — paste them into a blank note, one per line, labeled. You'll need 4 of them in the steps below:

   | Photo | I'll call it | Paste its URL here |
   |---|---|---|
   | library-logo.jpg | **LOGO-URL** | |
   | library-exterior.jpg | **EXTERIOR-URL** | |
   | library-exterior-sketch.jpg | **SKETCH-URL** | |
   | andrew_carnegie.jpg | **CARNEGIE-URL** | |
   | LibraryPassportLogo-removebg-preview.png | **PASSPORT-URL** | |

When a code block below says `LOGO-URL`, `EXTERIOR-URL`, etc., replace that word with the matching URL from your note.

## Step 4 — Paste the Header (once)

1. Go to **Appearance → Editor → Patterns → Template Parts → Header** (or **Templates → Header**). Delete anything already in there.
2. Click the **+** button, search for **Custom HTML**, add that block.
3. Paste the code below.
4. **Replace `LOGO-URL`** (near the top) with your logo URL from Step 3.
5. Click **Save**.

```html
<a class="skip-link" href="#main-content">Skip to main content</a>

<div class="topbar">
  📞 Curbside pickup &amp; book delivery available — call <a href="tel:+17654352700">765-435-2700</a>
</div>

<header class="site-header">
  <div class="header-inner">
    <a href="/" class="brand">
      <div class="brand-mark"><img src="LOGO-URL" alt="" aria-hidden="true" class="brand-logo-img"></div>
      <div class="brand-text">
        <div class="brand-name">Waveland-Brown Township Public Library</div>
        <div class="brand-tagline">A Carnegie Library &middot; Est. 1915</div>
      </div>
    </a>
  </div>
  <nav class="main-nav" aria-label="Main navigation">
    <div class="nav-inner">
      <button class="nav-toggle" type="button" aria-expanded="false" aria-controls="nav-menu">Menu</button>
      <ul id="nav-menu">
        <li><a href="/">Home</a></li>
        <li><a href="https://evergreen.lib.in.us/eg/opac/home" target="_blank" rel="noopener">Catalog<span class="visually-hidden"> (opens in new tab)</span></a></li>
        <li><a href="/events/">Events</a></li>
        <li><a href="/services/">Services</a></li>
        <li><a href="/research/">Research</a></li>
        <li><a href="/about/">About &amp; History</a></li>
        <li><a href="/policies/">Policies</a></li>
        <li><a href="/contact/">Contact</a></li>
      </ul>
    </div>
  </nav>
</header>

<script>
  document.documentElement.className += " js";
  (function () {
    var toggle = document.querySelector(".nav-toggle");
    var menu = document.getElementById("nav-menu");
    if (toggle && menu) {
      toggle.addEventListener("click", function () {
        var open = menu.classList.toggle("open");
        toggle.setAttribute("aria-expanded", open ? "true" : "false");
      });
    }
  })();
</script>
```

## Step 5 — Paste the Footer (once)

1. Go to **Appearance → Editor → Patterns → Template Parts → Footer**. Delete anything in there.
2. Add a **Custom HTML** block.
3. Paste the code below. (No URLs to change here.)
4. Click **Save**.

```html
<footer class="site-footer">
  <div class="container">
    <div class="footer-grid">
      <div>
        <h4>Waveland-Brown Township Public Library</h4>
        <p>115 Green St<br>Waveland, IN 47989</p>
        <p style="margin-top:0.5rem;">📞 <a href="tel:+17654352700">765-435-2700</a></p>
        <p style="margin-top:0.4rem;">📘 <a href="https://www.facebook.com/wavelandlibrary/" target="_blank" rel="noopener">Follow us on Facebook<span class="visually-hidden"> (opens in new tab)</span></a></p>
      </div>
      <div>
        <h4>Quick Links</h4>
        <ul>
          <li><a href="https://evergreen.lib.in.us/eg/opac/home" target="_blank" rel="noopener">Catalog<span class="visually-hidden"> (opens in new tab)</span></a></li>
          <li><a href="/events/">Events</a></li>
          <li><a href="/services/">Services</a></li>
          <li><a href="/research/">Research</a></li>
        </ul>
      </div>
      <div>
        <h4>About</h4>
        <ul>
          <li><a href="/about/">Our History</a></li>
          <li><a href="/about/#board">Board of Trustees</a></li>
          <li><a href="/policies/">Policies</a></li>
          <li><a href="/contact/">Contact Us</a></li>
        </ul>
      </div>
    </div>
    <div class="footer-bottom">
      <p class="a11y-note">We are committed to making our website accessible to everyone. If you have difficulty using any part of this site, please call <a href="tel:+17654352700">765-435-2700</a> and we will gladly assist you.</p>
      <p>&copy; 2026 Waveland-Brown Township Public Library &middot; A Carnegie Library serving the community since 1915</p>
    </div>
  </div>
</footer>
```

## Step 6 — Make the 8 pages

**Every page is the exact same 6 steps:**

1. **Pages → Add New Page**.
2. Type the **page title** (from the list below).
3. Click the **+**, search **Custom HTML**, add that one block.
4. Open the matching **`.html` file** from this project. Find the line `<main id="main-content">` near the top, and `</main>` near the bottom. **Select everything between those two tags** (not the tags themselves), copy it, and paste into the Custom HTML block.
5. **Make that page's fixes** (links and photos — see below).
6. Click **Publish**.

Repeat for all 8 pages in this table:

| Page title | Copy from this file | Photos to fix on this page |
|---|---|---|
| Home | `index.html` | `images/library-exterior.jpg` → **EXTERIOR-URL** |
| About & History | `about.html` | `images/library-exterior-sketch.jpg` → **SKETCH-URL**, and `images/andrew_carnegie.jpg` → **CARNEGIE-URL** |
| Services | `services.html` | `images/LibraryPassportLogo-removebg-preview.png` → **PASSPORT-URL** |
| Research | `research.html` | none |
| Policies | `policies.html` | none |
| Contact | `contact.html` | none |
| Events | `events.html` | none |

### The two fixes, explained

**Fix 1 — Photos.** Only Home, About, and Services have photos. In the pasted code, find the `images/...` filename (shown in the table above) and replace it with your URL from Step 3. For example, on the Home page, find:

```
src="images/library-exterior.jpg"
```
and change it to:
```
src="EXTERIOR-URL"
```
(using your real URL). The About page has **two** photos to fix.

> On the About page you may see a `<source srcset="images/andrew-carnegie-...avif" ...>` line just above the Carnegie photo. Simplest option: **delete that one `<source>` line entirely.** The regular `andrew_carnegie.jpg` below it will show fine.

**Fix 2 — Links.** The copied pages link to each other using old file names like `about.html`. WordPress uses addresses like `/about/`. In each page's pasted code, change any link that ends in `.html` using this table:

| Find this | Change it to |
|---|---|
| `index.html` | `/` |
| `about.html` | `/about/` |
| `about.html#board` | `/about/#board` |
| `events.html` | `/events/` |
| `services.html` | `/services/` |
| `research.html` | `/research/` |
| `policies.html` | `/policies/` |
| `contact.html` | `/contact/` |

(Links that start with `http` — the catalog, Facebook, T.C. Steele — stay exactly as they are. Don't touch those.)

> Tip: after pasting a page, glance through the code for `.html` and for `images/`. Those two things are the only edits you ever make. If you don't see either on a page, there's nothing to fix — just Publish.

## Step 7 — Set the homepage

1. Go to **Settings → Reading**.
2. Under "Your homepage displays," choose **A static page**, and set **Homepage** to **Home**.
3. Save.

Now visit your site. The header, footer, colors, and all 8 pages should be live.

## If something looks wrong

- **Everything is plain text, no colors** → the CSS in Step 2 didn't save, or the `@import` line is missing. Redo Step 2.
- **A photo shows a broken-image icon** → that page still has an `images/...` path you didn't replace with a URL (Fix 1).
- **A menu/link goes to a "page not found"** → that link still ends in `.html` (Fix 2). Also double-check each page's web address under its title matches the table (e.g., the Events page address should be `/events/`).
- **The header logo is missing** → the `LOGO-URL` in Step 4 wasn't replaced with the real URL.

---

## Optional, do this later: let staff edit Hours & Events without code

Everything above gets the site live. The trade-off is that the Hours table, Board/Staff lists, and Events are pasted as HTML — editable, but a careless deletion could nudge the layout.

Once the site is up and you want the director/aides to edit those **without touching code**, that part can be rebuilt with WordPress's native Table and Group blocks (point-and-click). It's a separate, more involved step — tell me when you're ready and I'll walk you through just those pieces. There's no rush, and the site works fine in the meantime.

## A note on the Carnegie photo

The Andrew Carnegie portrait file came from Getty Images (a stock-photo company). If this site is going fully public, double-check you're allowed to use it, or swap in a free public-domain portrait (Carnegie died in 1919, so old photos of him are free to use in the US). Just ask and I can find one.
