# Moving this site into WordPress

Goal: the visual design stays locked in (so it can't accidentally get broken), but **Hours, Board of Trustees, Library Staff, and Events** become real, point-and-click WordPress content that the director/aides can edit themselves — no HTML required.

## How it's split

| Content | How it's built | Who can edit it |
|---|---|---|
| Header, nav, footer, topbar banner | One Custom HTML block, set up once as Template Parts | You (rare — links/address almost never change) |
| Home/About/Services/Research/Policies/Contact body text | Custom HTML blocks (per page) | You, by carefully editing text between tags |
| **Hours** (Home + Contact) | Native **Table block** | **Staff — click a cell, type, done** |
| **Board of Trustees** (About) | Native **Table block** | **Staff** |
| **Library Staff** (About) | Native **Table block** | **Staff** |
| **Events listing** (Events page) | Native **Group + Heading + Paragraph blocks** | **Staff — add/remove/edit programs freely** |

---

## Step 1 — Pick a theme

You need a **block theme** (so Appearance → Editor exists, letting you set the header/footer once instead of per page). Two good options:

- **Blank Canvas** (search "Blank Canvas" in Appearance → Themes → Add New) — built specifically for sites with fully custom CSS, near-zero default styling.
- **Twenty Twenty-Four** — ships free with WordPress, also block-based.

Install and activate one. Then check the left sidebar for **Appearance → Editor**. If it's there, you're set. If you only see "Customize" (no "Editor"), the theme isn't block-based — go back and pick the other one.

> If your library's WordPress account doesn't let you install themes at all (some managed hosting locks this down), tell me what theme is currently active and I'll adjust the plan — everything below still works, just gets wired into whatever theme you've got via Additional CSS.

## Step 2 — Add the site CSS

Go to **Appearance → Editor → Styles → (the paintbrush/CSS icon) → Additional CSS** (or **Appearance → Customize → Additional CSS** on older WP). Paste the entire block below:

```css
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Source+Sans+3:wght@400;600;700&display=swap');

/* ===== paste everything from css/style.css below this line ===== */
```

Then open `css/style.css` in this project (656 lines) and paste its **entire contents** right after that line. That one file is what gives you the brick-red/golden-oak look, the cards, the timeline, the styled contact cards, the policy cards, the logo styling — all of it.

Add this small extra snippet at the very end, so the native Hours/Board/Staff tables match the site's style without any extra work:

```css
/* Style WordPress's native Table blocks to match the site */
.wp-block-table.hours-table table { width:100%; border-collapse:collapse; }
.wp-block-table.hours-table td, .wp-block-table.hours-table th { padding:0.45rem 0.6rem; border-bottom:1px dashed #e0d4bd; }
.wp-block-table.hours-table tr:last-child td { border-bottom:none; }
```

## Step 3 — Upload the images to the Media Library

The site now uses **real photos** (the old placeholders are gone). Before building the pages, upload each of these to **Media → Add New**, then click the uploaded file and copy its **File URL** — you'll paste those URLs into the HTML blocks later, replacing the `images/...` paths.

| File in this project | Where it's used | Replace this path with the Media URL |
|---|---|---|
| `images/library-logo.jpg` | Header brand mark (every page) | `images/library-logo.jpg` |
| `images/library-exterior.jpg` | Home — the photo beside the Emerson quote | `images/library-exterior.jpg` |
| `images/library-exterior-sketch.jpg` | About — Historical Photos (sketch card) | `images/library-exterior-sketch.jpg` |
| `images/andrew_carnegie.jpg` | About — Historical Photos (Carnegie card) | `images/andrew_carnegie.jpg` |
| `images/andrew-carnegie-gettyimages-640453979.avif` | About — Carnegie card, preferred format (optional) | `images/andrew-carnegie-gettyimages-640453979.avif` |
| `images/LibraryPassportLogo-removebg-preview.png` | Services — Indiana Library Passport card | `images/LibraryPassportLogo-removebg-preview.png` |

> **Tip:** keep a scratch note pairing each filename with the URL WordPress gives it (they look like `https://yoursite.org/wp-content/uploads/2026/06/library-logo.jpg`). Then it's a quick find-and-replace when you paste each block.

> **Two small notes on the Carnegie photo:** (1) The site uses a `<picture>` element that loads the modern `.avif` first and falls back to the `.jpg`. If that feels fussy, you can drop the `<source>` line and just use the `.jpg` — it looks identical. (2) That `.avif` is a Getty Images stock photo; if this goes on the public live site, confirm you have a license, or swap in a public-domain Carnegie portrait (he died in 1919, so pre-1929 images are public domain in the US). I can help find one.

## Step 4 — Build the Header (once)

Go to **Appearance → Editor → Templates → (or Template Parts) → Header**. Delete whatever's there, add a **Custom HTML** block, and paste the following — then replace `LIBRARY-LOGO-URL` with the Media Library URL for `library-logo.jpg` from Step 3:

```html
<a class="skip-link" href="#main-content">Skip to main content</a>

<div class="topbar">
  📞 Curbside pickup &amp; book delivery available — call <a href="tel:+17654352700">765-435-2700</a>
</div>

<header class="site-header">
  <div class="header-inner">
    <a href="/" class="brand">
      <div class="brand-mark"><img src="LIBRARY-LOGO-URL" alt="" aria-hidden="true" class="brand-logo-img"></div>
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

**Note:** I changed the links from `index.html`/`about.html` etc. to `/`, `/about/`, `/events/` style — that's how WordPress page URLs normally work. When you create each page in Step 6, check its actual URL slug (shown under the page title when editing) and fix these links if they don't match.

## Step 5 — Build the Footer (once)

**Appearance → Editor → Template Parts → Footer**. Custom HTML block:

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

Same note as above — fix the `/about/`, `/events/` etc. links once you know each page's real slug.

## Step 6 — Build each page

For each page below: **Pages → Add New**, give it the title shown, then add the blocks listed in order.

### Home (set as homepage in Settings → Reading)

1. **Custom HTML block** — the hero, mission, "Explore the Library" cards, and the start of the "Our Story" two-column row (this block leaves the `prose` column open; the hours panel comes next as a native block):
```html
<section class="hero">
  <span class="est">Serving Our Community Since 1915</span>
  <h1>A Place to Read, Learn,<br>and Gather</h1>
  <p class="lede">For over a century, our historic Carnegie library has been the heart of Waveland and Brown Township — a free library for everyone, just as it was promised in 1915.</p>
  <a href="https://evergreen.lib.in.us/eg/opac/home" class="btn btn-gold" target="_blank" rel="noopener">Search the Catalog</a>
  <a href="/contact/" class="btn btn-outline">Visit Us</a>
</section>

<section class="band">
  <div class="container center">
    <p class="section-kicker">Our Mission</p>
    <h2 class="section-title">Information, Education &amp; Community</h2>
    <p class="section-intro">The mission of the Waveland-Brown Township Public Library is to serve our community by providing information and resources for education and recreational needs. We hope to serve as a physical center where families and friends can gather, and to work closely with schools, churches, and other community groups.</p>
  </div>
</section>

<section class="band alt">
  <div class="container">
    <p class="section-kicker center" style="text-align:center;">What We Offer</p>
    <h2 class="section-title center" style="text-align:center;">Explore the Library</h2>
    <div class="card-grid">
      <div class="card">
        <div class="card-icon" aria-hidden="true">🔍</div>
        <h3>Browse the Catalog</h3>
        <p>Search our collection of books, audiobooks, movies, and more — and place holds from home.</p>
        <a class="card-link" href="https://evergreen.lib.in.us/eg/opac/home" target="_blank" rel="noopener">Search now</a>
      </div>
      <div class="card">
        <div class="card-icon" aria-hidden="true">📅</div>
        <h3>Events &amp; Programs</h3>
        <p>Story hours, community presentations, and board meetings — see what's happening this month.</p>
        <a class="card-link" href="/events/">View the calendar</a>
      </div>
      <div class="card">
        <div class="card-icon" aria-hidden="true">🚗</div>
        <h3>Curbside &amp; Delivery</h3>
        <p>Can't make it inside? Call us at 765-435-2700 to arrange curbside pickup or a book delivery.</p>
        <a class="card-link" href="/services/">Our services</a>
      </div>
      <div class="card">
        <div class="card-icon" aria-hidden="true">💡</div>
        <h3>Research &amp; Learning</h3>
        <p>Free access to online databases, homework help, and local history resources.</p>
        <a class="card-link" href="/research/">Start researching</a>
      </div>
    </div>
  </div>
</section>

<section class="band">
  <div class="container">
    <div class="two-col">
      <div class="prose">
        <p class="section-kicker">Our Story</p>
        <h2 class="section-title">A Carnegie Library, Built by the Community</h2>
        <p>The Waveland-Brown Township Public Library was built in Montgomery County, Indiana starting in the fall of 1914 using matching funds from Andrew Carnegie. The library has been serving the community since 1915 — and still operates from the original building.</p>
        <p>Step inside and you'll find the original golden oak woodwork, the first reading tables still in use, and a painting by world-renowned artist T.C. Steele — one of Waveland's most famous sons — hanging in its intended spot above the fireplace.</p>
        <a href="/about/" class="btn btn-brick">Read Our Full History</a>
      </div>
```
2. **Group block** — Advanced settings → Additional CSS class(es): `info-panel`. Inside it add:
   - **Heading block**: "Visit Us"
   - **Table block**, 2 columns × 7 rows. Advanced settings → Additional CSS class(es): `hours-table`. Fill in:

     | Day | Hours |
     |---|---|
     | Monday | 9:00 – 6:00 |
     | Tuesday | 9:00 – 6:00 |
     | Wednesday | 9:00 – 6:00 |
     | Thursday | 9:00 – 6:00 |
     | Friday | Closed |
     | Saturday | 9:00 – 1:00 |
     | Sunday | Closed |
   - **Paragraph block**: "Questions? Call 765-435-2700." (make the number a link to `tel:+17654352700`)
3. **Custom HTML block** — this closes the two-column row, then adds the **library photo + Emerson quote card** and the "Free Library Card" section. Replace `LIBRARY-EXTERIOR-URL` with the Media URL for `library-exterior.jpg`:
```html
    </div>

    <div class="two-col" style="margin-top:2rem; border:1px solid #e6dcc8; border-top:4px solid var(--oak); border-radius:6px; overflow:hidden; box-shadow:0 2px 8px rgba(84,33,26,0.07); gap:0;">
      <img src="LIBRARY-EXTERIOR-URL"
           alt="Front exterior of the Waveland-Brown Township Public Library Carnegie building"
           style="width:100%; height:100%; min-height:260px; object-fit:cover; display:block;">
      <div style="background:var(--white); padding:2rem; display:flex; align-items:center;">
        <blockquote style="font-family:var(--serif); font-style:italic; font-size:1.05rem; line-height:1.75; color:var(--ink); margin:0; border-left:4px solid var(--oak); padding-left:1.2rem;">
          "I cannot remember the books I've read any more than the meals I have eaten; even so, they have made me."
          <cite style="display:block; margin-top:1rem; font-style:normal; font-size:0.82rem; letter-spacing:0.1em; text-transform:uppercase; color:var(--ink-soft);">— Ralph Waldo Emerson, 1803–1882</cite>
        </blockquote>
      </div>
    </div>
  </div>
</section>

<section class="band alt">
  <div class="container center">
    <p class="section-kicker">Free for Everyone</p>
    <h2 class="section-title">Get Your Free Library Card</h2>
    <p class="section-intro">Waveland and Brown Township citizens have received free library cards since 1915 — and that remains our policy today. Stop in to sign up; all you need is proof of residence.</p>
    <a href="/contact/" class="btn btn-brick">Plan Your Visit</a>
  </div>
</section>
```

### About & History

1. **One big Custom HTML block** — copy `about.html` lines **51–189** straight across: the page-hero, Beginnings, The Carnegie Library Building (+ Building Facts), **Historical Photos** (sketch + Carnegie cards), Fun Facts grid, Celebrations timeline, and Librarians timeline. **Stop right before the Board of Trustees section.**
   - In the **Historical Photos** part, replace the two image paths with their Media URLs: `library-exterior-sketch.jpg` (sketch card) and `andrew_carnegie.jpg` (Carnegie card). If you kept the `<picture>`/`.avif` setup, also replace the `.avif` path in the `<source>` line; otherwise delete that `<source>` line and just use the `.jpg`.

2. **Board of Trustees** — a **Group block**, class `band alt`, containing a **Group** class `container`, containing:
   - Paragraph "Leadership" (class `section-kicker`), Heading "Board of Trustees" (class `section-title`), Paragraph with the board's meeting-schedule blurb
   - **Table block**, class `hours-table`, columns "Name" / "Role":

     | Name | Role |
     |---|---|
     | Kim Nixon | President |
     | Megan Fullenwider | Vice President |
     | Lorraine Waling | Secretary |
     | Sarah Phillips | Treasurer |
     | Donna Sabolick | Trustee |
     | Jerri King | Trustee |
     | Paula Finch | Trustee |

3. **Library Staff** — same Group + Table pattern:

     | Name | Role |
     |---|---|
     | Christy Roark | Director |
     | Carol Coffman | Library Aide |
     | Kerri Simpson | Library Aide |
     | Karen Myers | Library Aide |

4. **Final Custom HTML block** — the closing centennial pull-quote section (`about.html` lines **222–229**):
```html
<section class="band dark">
  <div class="container">
    <blockquote class="pull-quote">
      "The doctors and teachers are mainly gone and not too many businesses are left, but the people still try to take care of the library's needs 100 years later."
      <cite>— From our Centennial History</cite>
    </blockquote>
  </div>
</section>
```

### Services, Research, Policies

These barely ever change — paste the full `<main>...</main>` inner content (minus the page-hero-to-footer boilerplate you already know to strip) from `services.html`, `research.html`, `policies.html` into one Custom HTML block per page, unchanged.

- **Services:** includes the **Indiana Library Passport** card — remember to replace its image path with the Media URL for `LibraryPassportLogo-removebg-preview.png`.
- **Policies:** the policies are now a grid of styled cards (each with an emoji badge); it's all in that one Custom HTML block, nothing extra to wire up.

### Contact

One Custom HTML block for the page-hero and the Visit / Call / Facebook cards, and the map iframe — but **skip the "Hours" card** in `contact-grid`. After the Custom HTML block, add the Hours as a native block so staff can edit it:

- **Group block**, class `contact-item`, containing:
  - Paragraph: "🕐" (class `big-icon`)
  - Heading: "Hours"
  - **Table block**, class `hours-table` (same 7 rows as the Home page table above)

Then a final Custom HTML block with the map and the "Our Historic Building" two-column section (the last `<section>` near the end of `contact.html`).

### Events — the one that changes most often

Custom HTML block for the page-hero and the board-meeting notice banner (`events.html` top). Then build the program list as real blocks so the director can edit it freely:

- **Group block**, class `card-grid`. Inside, add one **Group block per program**, each with class `card`, each containing:
  - Paragraph with just the emoji (class `card-icon`)
  - Heading with the program name
  - Paragraph with the description

  Starting content (replace with whatever's actually happening that month):

  | Icon | Title | Description |
  |---|---|---|
  | 🧒 | Children's Story Hour | Stories, songs, and crafts for our youngest readers in the children's section. Call the library for this month's schedule. |
  | 🏛️ | Board of Trustees Meeting | Last Tuesday of every month at the library. Open to the public — agendas available at the front desk. |
  | 📖 | Summer Reading Program | Reading challenges and prizes for kids and teens all summer long. Sign up at the front desk. |
  | 🎬 | Community Programs | Movies, presentations, and special guests in our historic downstairs meeting room — just as it's been for eleven decades. |

  From now on, staff can duplicate one of these Group blocks, change the text, or delete one entirely — no code.

## Step 7 — Menus and homepage

- **Appearance → Menus** (or the Navigation block if your theme uses one) — only needed if your theme requires a separate registered menu; since the nav is hardcoded into the Header template part above, you likely don't need this.
- **Settings → Reading** — set the Home page as your homepage.

## A note on what you're trading off

This setup makes Hours/Board/Staff/Events fully staff-safe. Everything else (page layout, header, footer, the photos, the Services/Research/Policies wording) still lives in Custom HTML blocks — editable, but a wrong deleted tag could break the layout. That's an intentional choice: that content almost never changes, so it's not worth the much larger effort of converting every paragraph into native blocks. If that ever turns out to be wrong (e.g. policies need frequent updates), the same Group+Paragraph technique used for Events can be applied there too.

Photos going forward: when you want to swap a photo, the WordPress-native way is **Media Library → upload → copy File URL → paste it over the old URL** in the relevant Custom HTML block. (Or, for a spot you expect staff to change often, replace that `<img>` with a native **Image block**, which is fully click-to-edit.)
