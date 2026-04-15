# Adam Guo Portfolio — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a pixel-faithful single-page portfolio website for Adam Guo from the Pencil design, using plain HTML + CSS with Web3Forms for contact.

**Architecture:** Two files (`index.html` + `styles.css`) plus an `images/` folder. All design tokens live in `:root` CSS variables. Responsive via a single 768px media query — everything stacks on mobile. No JavaScript except Lucide CDN icon init.

**Tech Stack:** HTML5, CSS3 (custom properties, flexbox, keyframe animations), Lucide icons via CDN, Web3Forms for contact form submission.

---

## File Map

| File | Responsibility |
|---|---|
| `index.html` | All markup — 7 sections, Web3Forms form, Lucide icon tags |
| `styles.css` | All styles — `:root` variables, section styles, component styles, 768px media query |
| `images/portrait.png` | Hero portrait photo (Adam provides this) |

Performance card images and Spotify artist photo are remote URLs — no local image files needed for those.

---

### Task 1: Project scaffold + CSS variables

**Files:**
- Create: `index.html`
- Create: `styles.css`

- [ ] **Step 1: Create `index.html` with boilerplate, font imports, and empty section stubs**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Adam Guo — Portfolio</title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400&family=DM+Mono:wght@300;400;500&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
  <script src="https://unpkg.com/lucide@latest"></script>
  <link rel="stylesheet" href="styles.css">
</head>
<body>

  <section id="hero">
    <!-- nav + hero content go here -->
  </section>

  <section id="ticker">
    <!-- trust ticker -->
  </section>

  <section id="what-i-offer">
    <!-- pillar cards -->
  </section>

  <section id="performances">
    <!-- performance cards -->
  </section>

  <section id="contact">
    <!-- contact info + form -->
  </section>

  <footer id="footer">
    <!-- footer -->
  </footer>

  <script>lucide.createIcons();</script>
</body>
</html>
```

- [ ] **Step 2: Create `styles.css` with all CSS variables and a base reset**

```css
/* =====================
   CSS VARIABLES
   ===================== */
:root {
  /* Colors */
  --color-cream:          #F7F4EE;
  --color-warm-gray:      #F2EFE8;
  --color-dark:           #1A1A18;
  --color-separator:      #D8D3C8;
  --color-text-secondary: #6B6560;
  --color-text-muted:     #9A9488;
  --color-text-faint:     #C0BAB0;
  --color-input-bg:       #242420;
  --color-input-border:   #5A5550;
  --color-card-border:    #E0DBD2;
  --color-card-divider:   #E8E3DA;
  --color-tag-text:       #7A7268;

  /* Buttons */
  --btn-primary-bg:   var(--color-dark);
  --btn-primary-text: var(--color-cream);
  --btn-submit-bg:    var(--color-cream);
  --btn-submit-text:  var(--color-dark);

  /* Fonts */
  --font-display: 'Cormorant Garamond', serif;
  --font-body:    'DM Sans', sans-serif;
  --font-mono:    'DM Mono', monospace;

  /* Section spacing */
  --padding-section-x: 120px;
  --padding-section-y: 72px;
  --padding-nav-x:     64px;
  --padding-footer-x:  80px;

  /* Gaps */
  --gap-hero-content:  20px;
  --gap-hero-cta:      24px;
  --gap-nav-links:     32px;
  --gap-pillars-grid:  1px;
  --gap-cards-grid:    16px;
  --gap-contact:       80px;
  --gap-contact-info:  24px;
  --gap-form-fields:   20px;
  --gap-form-name-row: 16px;
  --gap-social-links:  24px;
  --gap-ticker:        28px;

  /* Component padding */
  --padding-pillar-card: 32px;
  --padding-card-body:   20px;
  --padding-btn-primary: 13px 28px;
  --padding-btn-submit:  14px 28px;
  --padding-input:       10px 12px;
  --padding-chip:        3px 8px;
}

/* =====================
   BASE RESET
   ===================== */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  scroll-behavior: smooth;
}

body {
  font-family: var(--font-body);
  background-color: var(--color-cream);
  color: var(--color-dark);
  max-width: 1440px;
  margin: 0 auto;
  overflow-x: hidden;
}

a {
  text-decoration: none;
  color: inherit;
}

button {
  cursor: pointer;
  border: none;
  font-family: var(--font-body);
}
```

- [ ] **Step 3: Open `index.html` in a browser — verify the page is blank with a cream background and no console errors**

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "feat: scaffold project with CSS variables and base reset"
```

---

### Task 2: Nav

**Files:**
- Modify: `index.html` — fill in the nav inside `#hero`
- Modify: `styles.css` — add nav styles

- [ ] **Step 1: Add nav markup inside `#hero`**

```html
<section id="hero">
  <header class="nav">
    <a href="#" class="nav__logo">ADAM GUO</a>
    <nav class="nav__links">
      <a href="#what-i-offer">WHAT I OFFER</a>
      <a href="#performances">PERFORMANCES</a>
      <a href="#contact">CONTACT</a>
    </nav>
  </header>
</section>
```

- [ ] **Step 2: Add nav styles to `styles.css`**

```css
/* =====================
   NAV
   ===================== */
.nav {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 64px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 var(--padding-nav-x);
  z-index: 10;
}

.nav__logo {
  font-family: var(--font-body);
  font-size: 13px;
  font-weight: 500;
  letter-spacing: 6px;
  color: var(--color-dark);
}

.nav__links {
  display: flex;
  gap: var(--gap-nav-links);
}

.nav__links a {
  font-family: var(--font-body);
  font-size: 12px;
  font-weight: 300;
  letter-spacing: 1px;
  color: var(--color-text-muted);
}
```

- [ ] **Step 3: Open in browser — verify logo left, links right, correct fonts and spacing**

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "feat: add nav"
```

---

### Task 3: Hero section

**Files:**
- Modify: `index.html` — add portrait, gradient overlays, hero content
- Modify: `styles.css` — add hero styles

- [ ] **Step 1: Add full hero markup**

Replace the `#hero` section with:

```html
<section id="hero">
  <header class="nav">
    <a href="#" class="nav__logo">ADAM GUO</a>
    <nav class="nav__links">
      <a href="#what-i-offer">WHAT I OFFER</a>
      <a href="#performances">PERFORMANCES</a>
      <a href="#contact">CONTACT</a>
    </nav>
  </header>

  <div class="hero__portrait"></div>
  <div class="hero__gradient hero__gradient--top"></div>
  <div class="hero__gradient hero__gradient--right"></div>
  <div class="hero__gradient hero__gradient--bottom"></div>
  <div class="hero__gradient hero__gradient--left"></div>

  <div class="hero__content">
    <p class="hero__eyebrow">SOLOIST — CHAMBER MUSICIAN — RECORDING ARTIST</p>
    <h1 class="hero__heading">Hi, I'm Adam Guo</h1>
    <div class="hero__body">
      <p>I have been teaching violin and piano for over six years, bringing both technical expertise and genuine passion to his instruction.</p>
      <p>I hold a Master's degree in Violin Performance from the Mannes School of Music, where I studied under Michelle Kim, Assistant Concertmaster of the New York Philharmonic.</p>
    </div>
    <div class="hero__cta">
      <a href="#contact" class="btn-primary">Contact</a>
      <a href="https://open.spotify.com/artist/51akc10V0N4dEo8GUC8am7" target="_blank" class="hero__spotify-link">Listen on Spotify →</a>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add hero styles**

```css
/* =====================
   HERO
   ===================== */
#hero {
  position: relative;
  height: 720px;
  overflow: hidden;
  background-color: var(--color-cream);
}

.hero__portrait {
  position: absolute;
  top: 0;
  right: 0;
  width: 741px;
  height: 720px;
  background-image: url('images/portrait.png');
  background-size: cover;
  background-position: center top;
  z-index: 0;
}

.hero__gradient {
  position: absolute;
  z-index: 1;
  pointer-events: none;
}

.hero__gradient--top {
  top: 0; left: 0; right: 0;
  height: 300px;
  background: linear-gradient(to bottom, #F7F4EE 0%, #F7F4EECC 20%, #F7F4EE88 50%, #F7F4EE11 80%, #F7F4EE00 100%);
}

.hero__gradient--bottom {
  bottom: 0; left: 0; right: 0;
  height: 300px;
  background: linear-gradient(to top, #F7F4EE 0%, #F7F4EECC 20%, #F7F4EE80 50%, #F7F4EE00 100%);
}

.hero__gradient--right {
  top: 0; right: 0; bottom: 0;
  width: 400px;
  background: linear-gradient(to left, #F7F4EE 0%, #F7F4EEB3 30%, #F7F4EE80 60%, #F7F4EE00 100%);
}

.hero__gradient--left {
  top: 0; left: 0; bottom: 0;
  width: 400px;
  background: linear-gradient(to right, #F7F4EE 0%, #F7F4EEB3 30%, #F7F4EE80 60%, #F7F4EE00 100%);
}

.hero__content {
  position: relative;
  z-index: 2;
  padding: 160px var(--padding-section-x) 0;
  display: flex;
  flex-direction: column;
  gap: var(--gap-hero-content);
}

.hero__eyebrow {
  font-family: var(--font-mono);
  font-size: 10px;
  font-weight: 400;
  letter-spacing: 3px;
  color: var(--color-text-muted);
}

.hero__heading {
  font-family: var(--font-display);
  font-size: 96px;
  font-weight: 300;
  line-height: 0.93;
  max-width: 443px;
  color: var(--color-dark);
}

.hero__body {
  display: flex;
  flex-direction: column;
  gap: 12px;
  max-width: 520px;
}

.hero__body p {
  font-family: var(--font-body);
  font-size: 15px;
  font-weight: 300;
  line-height: 1.7;
  color: var(--color-text-secondary);
}

.hero__cta {
  display: flex;
  align-items: center;
  gap: var(--gap-hero-cta);
}

.btn-primary {
  display: inline-block;
  background-color: var(--btn-primary-bg);
  color: var(--btn-primary-text);
  padding: var(--padding-btn-primary);
  font-family: var(--font-body);
  font-size: 10px;
  font-weight: 500;
  letter-spacing: 2px;
}

.hero__spotify-link {
  font-family: var(--font-mono);
  font-size: 12px;
  font-weight: 300;
  letter-spacing: 0.5px;
  color: #4b4b4b;
}
```

- [ ] **Step 3: Add `images/portrait.png`** — drop Adam's photo into the `images/` folder named `portrait.png`

- [ ] **Step 4: Open in browser — verify portrait on right, gradients blending into cream, heading/body/CTA stacked on left**

- [ ] **Step 5: Commit**

```bash
git add index.html styles.css images/portrait.png
git commit -m "feat: add hero section"
```

---

### Task 4: Trust Ticker

**Files:**
- Modify: `index.html` — fill in `#ticker`
- Modify: `styles.css` — add ticker styles + mobile scroll animation

- [ ] **Step 1: Add ticker markup** — items are doubled for the seamless mobile scroll loop

```html
<section id="ticker">
  <div class="ticker__track">
    <!-- Set 1 -->
    <div class="ticker__item">
      <span class="ticker__primary">NEW SCHOOL</span>
      <span class="ticker__secondary">ALUMNI '25</span>
    </div>
    <div class="ticker__divider"></div>
    <div class="ticker__item">
      <span class="ticker__primary">EAST BRUNSWICK SYMPHONY ORCHESTRA</span>
      <span class="ticker__secondary">VIOLINIST</span>
    </div>
    <div class="ticker__divider"></div>
    <div class="ticker__item">
      <span class="ticker__primary">STUDIO OF MICHELLE KIM</span>
    </div>
    <div class="ticker__divider"></div>
    <div class="ticker__item">
      <span class="ticker__primary">B.M.M.M</span>
    </div>
    <div class="ticker__divider"></div>
    <div class="ticker__item">
      <span class="ticker__primary">MUSICIAN</span>
    </div>
    <!-- Set 2 (duplicate for seamless loop on mobile) -->
    <div class="ticker__divider"></div>
    <div class="ticker__item">
      <span class="ticker__primary">NEW SCHOOL</span>
      <span class="ticker__secondary">ALUMNI '25</span>
    </div>
    <div class="ticker__divider"></div>
    <div class="ticker__item">
      <span class="ticker__primary">EAST BRUNSWICK SYMPHONY ORCHESTRA</span>
      <span class="ticker__secondary">VIOLINIST</span>
    </div>
    <div class="ticker__divider"></div>
    <div class="ticker__item">
      <span class="ticker__primary">STUDIO OF MICHELLE KIM</span>
    </div>
    <div class="ticker__divider"></div>
    <div class="ticker__item">
      <span class="ticker__primary">B.M.M.M</span>
    </div>
    <div class="ticker__divider"></div>
    <div class="ticker__item">
      <span class="ticker__primary">MUSICIAN</span>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add ticker styles**

```css
/* =====================
   TRUST TICKER
   ===================== */
#ticker {
  background-color: var(--color-dark);
  height: 52px;
  overflow: hidden;
}

.ticker__track {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 100%;
  padding: 0 var(--padding-nav-x);
  gap: var(--gap-ticker);
}

.ticker__item {
  display: flex;
  flex-direction: column;
  gap: 2px;
  white-space: nowrap;
  flex-shrink: 0;
}

.ticker__primary {
  font-family: var(--font-mono);
  font-size: 10px;
  font-weight: 500;
  letter-spacing: 2px;
  color: var(--color-text-faint);
}

.ticker__secondary {
  font-family: var(--font-mono);
  font-size: 10px;
  font-weight: 400;
  letter-spacing: 2px;
  color: #7A7268;
}

.ticker__divider {
  width: 1px;
  height: 10px;
  background-color: rgba(255, 255, 255, 0.3);
  flex-shrink: 0;
}
```

- [ ] **Step 3: Open in browser — verify dark bar with credentials spread across, white dividers between items**

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "feat: add trust ticker"
```

---

### Task 5: What I Offer

**Files:**
- Modify: `index.html` — fill in `#what-i-offer`
- Modify: `styles.css` — add pillar styles

- [ ] **Step 1: Add What I Offer markup**

```html
<section id="what-i-offer">
  <p class="section-label">WHAT I OFFER</p>
  <div class="pillars">
    <div class="pillar">
      <span class="pillar__number">01</span>
      <h3 class="pillar__title">Violin Lessons</h3>
      <p class="pillar__body">I have 6 years of experience with over 50 students ranging from ages young children to adults.</p>
    </div>
    <div class="pillar">
      <span class="pillar__number">02</span>
      <h3 class="pillar__title">Piano Lessons</h3>
      <p class="pillar__body">I have 8 years of experience playing the piano and have trained classically both throughout high school and music conservatory.</p>
    </div>
    <div class="pillar">
      <span class="pillar__number">03</span>
      <h3 class="pillar__title">Voice Training</h3>
      <p class="pillar__body">With operatic training through high school and into college, I am able to offer lessons for any prospective students.</p>
    </div>
  </div>
</section>
```

- [ ] **Step 2: Add What I Offer styles**

```css
/* =====================
   SHARED: SECTION LABEL
   ===================== */
.section-label {
  font-family: var(--font-mono);
  font-size: 10px;
  font-weight: 500;
  letter-spacing: 3px;
  color: var(--color-text-muted);
}

/* =====================
   WHAT I OFFER
   ===================== */
#what-i-offer {
  background-color: var(--color-cream);
  padding: var(--padding-section-y) var(--padding-section-x);
  display: flex;
  flex-direction: column;
  gap: 32px;
}

.pillars {
  display: flex;
  background-color: var(--color-separator);
  gap: var(--gap-pillars-grid);
}

.pillar {
  flex: 1;
  background-color: var(--color-cream);
  padding: var(--padding-pillar-card);
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.pillar__number {
  font-family: var(--font-mono);
  font-size: 10px;
  font-weight: 300;
  letter-spacing: 1px;
  color: var(--color-text-faint);
}

.pillar__title {
  font-family: var(--font-display);
  font-size: 26px;
  font-weight: 400;
  color: var(--color-dark);
}

.pillar__body {
  font-family: var(--font-body);
  font-size: 12px;
  font-weight: 300;
  line-height: 1.7;
  color: var(--color-text-muted);
}
```

- [ ] **Step 3: Open in browser — verify 3 equal columns with 1px separator lines, correct numbering and typography**

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "feat: add what i offer section"
```

---

### Task 6: Featured Performances

**Files:**
- Modify: `index.html` — fill in `#performances`
- Modify: `styles.css` — add card styles

- [ ] **Step 1: Add Performances markup**

```html
<section id="performances">
  <h2 class="performances__heading">Featured Performances</h2>
  <div class="cards">

    <div class="card">
      <div class="card__image" style="background-image: url('https://img.youtube.com/vi/HU9k3WdWd6I/maxresdefault.jpg')"></div>
      <hr class="card__divider">
      <div class="card__body">
        <p class="card__platform">YouTube</p>
        <div class="card__chips">
          <span class="chip">Solo Recital</span>
          <span class="chip">Baroque</span>
        </div>
        <p class="card__status">YOUTUBE</p>
      </div>
    </div>

    <div class="card">
      <div class="card__image" style="background-image: url('https://img.youtube.com/vi/IN5kOooVeF8/maxresdefault.jpg')"></div>
      <hr class="card__divider">
      <div class="card__body">
        <p class="card__platform">YouTube</p>
        <div class="card__chips">
          <span class="chip">Concerto</span>
          <span class="chip">Romantic</span>
          <span class="chip">Orchestral</span>
        </div>
        <p class="card__status">YOUTUBE</p>
      </div>
    </div>

    <div class="card">
      <div class="card__image" style="background-image: url('https://i.scdn.co/image/ab67616d00001e02ea57896b4f072641ad3fccf7')"></div>
      <hr class="card__divider">
      <div class="card__body">
        <p class="card__platform">Spotify</p>
        <div class="card__chips">
          <span class="chip">Chamber Music</span>
          <span class="chip">Impressionist</span>
        </div>
        <p class="card__status">SPOTIFY</p>
      </div>
    </div>

  </div>
</section>
```

- [ ] **Step 2: Add Performances styles**

```css
/* =====================
   FEATURED PERFORMANCES
   ===================== */
#performances {
  background-color: var(--color-warm-gray);
  padding: var(--padding-section-y) var(--padding-section-x);
  display: flex;
  flex-direction: column;
  gap: 40px;
}

.performances__heading {
  font-family: var(--font-display);
  font-size: 32px;
  font-weight: 300;
  color: var(--color-dark);
}

.cards {
  display: flex;
  gap: var(--gap-cards-grid);
}

.card {
  flex: 1;
  border: 1px solid var(--color-card-border);
  background-color: var(--color-cream);
  display: flex;
  flex-direction: column;
}

.card__image {
  height: 180px;
  background-size: cover;
  background-position: center;
}

.card__divider {
  border: none;
  border-top: 1px solid var(--color-card-divider);
}

.card__body {
  padding: var(--padding-card-body);
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.card__platform {
  font-family: var(--font-body);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.5px;
  color: var(--color-dark);
}

.card__chips {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.chip {
  font-family: var(--font-mono);
  font-size: 8px;
  font-weight: 400;
  letter-spacing: 1px;
  color: var(--color-tag-text);
  border: 1px solid var(--color-card-border);
  padding: var(--padding-chip);
}

.card__status {
  font-family: var(--font-mono);
  font-size: 9px;
  font-weight: 400;
  letter-spacing: 1.5px;
  color: var(--color-text-muted);
}
```

- [ ] **Step 3: Open in browser — verify 3 cards with YouTube/Spotify thumbnails loading, chips, correct background color on section**

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "feat: add featured performances section"
```

---

### Task 7: Contact section

**Files:**
- Modify: `index.html` — fill in `#contact`
- Modify: `styles.css` — add contact styles

- [ ] **Step 1: Add Contact markup**

Replace `YOUR_ACCESS_KEY` with Adam's actual Web3Forms key once he signs up at web3forms.com.

```html
<section id="contact">

  <div class="contact__info">
    <p class="contact__label">GET IN TOUCH</p>
    <h2 class="contact__heading">Contact:</h2>
    <div class="contact__details">
      <p class="contact__detail">adamguo09@gmail.com</p>
      <p class="contact__detail">917-213-8717</p>
    </div>
    <p class="contact__body">For any inquiries please contact me by phone and email and I will get back to you as soon as I can!</p>
    <div class="contact__socials">
      <!-- TODO: replace href with Adam's actual Instagram URL -->
      <a href="https://www.instagram.com" target="_blank" class="social-link">
        <i data-lucide="instagram"></i>
        <span>Instagram</span>
      </a>
      <a href="https://open.spotify.com/artist/51akc10V0N4dEo8GUC8am7" target="_blank" class="social-link">
        <i data-lucide="music"></i>
        <span>Spotify</span>
      </a>
      <!-- TODO: replace href with Adam's actual YouTube channel URL -->
      <a href="https://www.youtube.com" target="_blank" class="social-link">
        <i data-lucide="youtube"></i>
        <span>YouTube</span>
      </a>
    </div>
  </div>

  <form class="contact__form" action="https://api.web3forms.com/submit" method="POST">
    <input type="hidden" name="access_key" value="YOUR_ACCESS_KEY">
    <input type="hidden" name="subject" value="New message from Adam Guo portfolio">
    <div class="form__name-row">
      <div class="form__field">
        <label for="first-name">First Name</label>
        <input type="text" id="first-name" name="first_name" placeholder="Adam" required>
      </div>
      <div class="form__field">
        <label for="last-name">Last Name</label>
        <input type="text" id="last-name" name="last_name" placeholder="Guo" required>
      </div>
    </div>
    <div class="form__field">
      <label for="email">Email</label>
      <input type="email" id="email" name="email" placeholder="your@email.com" required>
    </div>
    <div class="form__field">
      <label for="subject">Subject</label>
      <input type="text" id="subject" name="subject_line" placeholder="Concert booking inquiry">
    </div>
    <div class="form__field">
      <label for="message">Message</label>
      <textarea id="message" name="message" placeholder="Tell me about your event or project..." required></textarea>
    </div>
    <button type="submit" class="btn-submit">SEND MESSAGE</button>
  </form>

</section>
```

- [ ] **Step 2: Add Contact styles**

```css
/* =====================
   CONTACT
   ===================== */
#contact {
  background-color: var(--color-dark);
  padding: 88px var(--padding-section-x);
  display: flex;
  gap: var(--gap-contact);
  align-items: flex-start;
}

.contact__info {
  width: 480px;
  flex-shrink: 0;
  display: flex;
  flex-direction: column;
  gap: var(--gap-contact-info);
}

.contact__label {
  font-family: var(--font-mono);
  font-size: 9px;
  font-weight: 500;
  letter-spacing: 3px;
  color: #ffffff;
}

.contact__heading {
  font-family: var(--font-display);
  font-size: 52px;
  font-weight: 300;
  line-height: 1.05;
  color: #E0DBD0;
}

.contact__details {
  display: flex;
  flex-direction: column;
  gap: 4px;
}

.contact__detail {
  font-family: var(--font-mono);
  font-size: 24px;
  font-weight: 300;
  color: var(--color-text-faint);
}

.contact__body {
  font-family: var(--font-body);
  font-size: 14px;
  line-height: 1.7;
  color: var(--color-tag-text);
  max-width: 400px;
}

.contact__socials {
  display: flex;
  gap: var(--gap-social-links);
}

.social-link {
  display: flex;
  align-items: center;
  gap: 6px;
  color: var(--color-tag-text);
}

.social-link i {
  width: 14px;
  height: 14px;
  color: var(--color-tag-text);
}

.social-link span {
  font-family: var(--font-mono);
  font-size: 11px;
  font-weight: 300;
  letter-spacing: 1px;
}

/* Form */
.contact__form {
  flex: 1;
  display: flex;
  flex-direction: column;
  gap: var(--gap-form-fields);
}

.form__name-row {
  display: flex;
  gap: var(--gap-form-name-row);
}

.form__name-row .form__field {
  flex: 1;
}

.form__field {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.form__field label {
  font-family: var(--font-body);
  font-size: 12px;
  font-weight: 500;
  color: var(--color-text-faint);
}

.form__field input,
.form__field textarea {
  background-color: var(--color-input-bg);
  border: 1px solid var(--color-input-border);
  border-radius: 6px;
  padding: var(--padding-input);
  color: var(--color-text-faint);
  font-family: var(--font-body);
  font-size: 13px;
  width: 100%;
  outline: none;
}

.form__field input::placeholder,
.form__field textarea::placeholder {
  color: var(--color-input-border);
}

.form__field textarea {
  height: 120px;
  resize: vertical;
  padding: 8px 12px;
}

.btn-submit {
  width: 100%;
  background-color: var(--btn-submit-bg);
  color: var(--btn-submit-text);
  padding: var(--padding-btn-submit);
  font-family: var(--font-body);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 2px;
}
```

- [ ] **Step 3: Open in browser — verify dark section, info on left (480px), form on right, all inputs styled dark with faint borders**

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "feat: add contact section with Web3Forms"
```

---

### Task 8: Footer

**Files:**
- Modify: `index.html` — fill in `#footer`
- Modify: `styles.css` — add footer styles

- [ ] **Step 1: Add footer markup**

```html
<footer id="footer">
  <span class="footer__logo">ADAM GUO</span>
  <span class="footer__copy">© 2026 Adam Guo. All rights reserved.</span>
</footer>
```

- [ ] **Step 2: Add footer styles**

```css
/* =====================
   FOOTER
   ===================== */
#footer {
  background-color: var(--color-dark);
  height: 64px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 var(--padding-footer-x);
}

.footer__logo {
  font-family: var(--font-body);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 5px;
  color: #5A5550;
}

.footer__copy {
  font-family: var(--font-mono);
  font-size: 9px;
  font-weight: 300;
  letter-spacing: 1px;
  color: #4A4540;
}
```

- [ ] **Step 3: Open in browser — verify dark footer, logo left, copyright right**

- [ ] **Step 4: Commit**

```bash
git add index.html styles.css
git commit -m "feat: add footer"
```

---

### Task 9: Responsive breakpoints (≤ 768px)

**Files:**
- Modify: `styles.css` — add `@media (max-width: 768px)` block at the bottom
- Modify: `index.html` — no changes needed (ticker duplication already done in Task 4)

- [ ] **Step 1: Add the full mobile media query block at the bottom of `styles.css`**

```css
/* =====================
   RESPONSIVE — ≤ 768px
   ===================== */
@media (max-width: 768px) {

  /* Nav */
  .nav {
    flex-direction: column;
    justify-content: center;
    gap: 12px;
    height: auto;
    padding: 16px;
    position: relative;
  }

  .nav__logo {
    font-size: 11px;
  }

  .nav__links {
    gap: 20px;
  }

  /* Hero */
  #hero {
    height: auto;
    padding-bottom: 48px;
  }

  .hero__portrait,
  .hero__gradient {
    display: none;
  }

  .hero__content {
    padding: 24px 24px 0;
  }

  .hero__heading {
    font-size: 48px;
  }

  /* Ticker — switch to scrolling marquee */
  #ticker {
    height: 52px;
  }

  .ticker__track {
    display: flex;
    justify-content: flex-start;
    padding: 0;
    width: max-content;
    animation: ticker-scroll 20s linear infinite;
  }

  .ticker__item {
    padding: 0 var(--gap-ticker);
  }

  @keyframes ticker-scroll {
    from { transform: translateX(0); }
    to   { transform: translateX(-50%); }
  }

  /* What I Offer */
  .pillars {
    flex-direction: column;
    background-color: transparent;
    gap: 0;
  }

  .pillar {
    border-bottom: 1px solid var(--color-separator);
  }

  .pillar:last-child {
    border-bottom: none;
  }

  #what-i-offer {
    padding: 48px 24px;
  }

  /* Performances */
  .cards {
    flex-direction: column;
  }

  #performances {
    padding: 48px 24px;
  }

  /* Contact */
  #contact {
    flex-direction: column;
    padding: 48px 24px;
    gap: 40px;
  }

  .contact__info {
    width: 100%;
  }

  .contact__detail {
    font-size: 18px;
  }

  /* Footer */
  #footer {
    flex-direction: column;
    justify-content: center;
    gap: 8px;
    height: auto;
    padding: 20px 16px;
    text-align: center;
  }
}
```

- [ ] **Step 2: Open browser, resize window to 600px wide — verify:**
  - Nav stacks vertically
  - Hero portrait hidden, content full-width
  - Ticker scrolls automatically
  - Pillar cards stack vertically with border separators
  - Performance cards stack vertically
  - Contact stacks (info then form)
  - Footer stacks

- [ ] **Step 3: Commit**

```bash
git add styles.css
git commit -m "feat: add responsive breakpoints at 768px"
```

---

### Task 10: Web3Forms — connect + test

**Files:**
- Modify: `index.html` — replace `YOUR_ACCESS_KEY` with real key

- [ ] **Step 1: Adam signs up at web3forms.com** with his email (`adamguo09@gmail.com`)

- [ ] **Step 2: Copy the access key from the Web3Forms dashboard**

- [ ] **Step 3: Replace `YOUR_ACCESS_KEY` in `index.html`**

Find this line:
```html
<input type="hidden" name="access_key" value="YOUR_ACCESS_KEY">
```
Replace `YOUR_ACCESS_KEY` with the actual key from Web3Forms.

- [ ] **Step 4: Test the form** — fill in all fields on the live page and click SEND MESSAGE. Verify Adam receives an email at `adamguo09@gmail.com`.

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: connect Web3Forms contact form"
```

---

### Task 11: Final review

- [ ] **Step 1: Desktop review (1440px)** — scroll through all 6 sections, check fonts, colors, spacing against the Pencil design

- [ ] **Step 2: Mobile review (375px)** — verify ticker scrolls, portrait hidden, all sections stack cleanly

- [ ] **Step 3: Cross-browser check** — open in Chrome, Firefox, Safari (or Edge). Verify nothing breaks.

- [ ] **Step 4: Fix typo check** — confirm "Violin Lessons" (not "Lessions") appears in the rendered page

- [ ] **Step 5: Update social links** — replace the Instagram and YouTube placeholder `href` values with Adam's actual profile URLs

- [ ] **Step 6: Final commit**

```bash
git add -A
git commit -m "chore: final polish and review"
```
