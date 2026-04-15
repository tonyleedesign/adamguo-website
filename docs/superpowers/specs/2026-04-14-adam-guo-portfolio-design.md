# Adam Guo Portfolio — Design Spec
**Date:** 2026-04-14
**Stack:** Plain HTML + CSS (no build tooling)
**Form service:** Web3Forms (free tier, 250 submissions/month)

---

## Overview

A single-page portfolio website for Adam Guo, a violinist, pianist, and voice teacher. The design is pixel-faithful to the Pencil canvas (`adamwebsite.pen`). Six sections stack vertically at a 1440px design width.

---

## File Structure

```
adamguo/
├── index.html
├── styles.css
└── images/
    ├── portrait.png          (hero photo)
    ├── performance-1.png
    ├── performance-2.png
    └── performance-3.png
```

---

## CSS Variables (`:root`)

All design tokens are defined as CSS custom properties. No raw hex values or magic numbers anywhere else in the stylesheet.

```css
:root {
  /* Colors */
  --color-cream:           #F7F4EE;
  --color-warm-gray:       #F2EFE8;
  --color-dark:            #1A1A18;
  --color-separator:       #D8D3C8;
  --color-text-secondary:  #6B6560;
  --color-text-muted:      #9A9488;
  --color-text-faint:      #C0BAB0;
  --color-input-bg:        #242420;
  --color-input-border:    #5A5550;
  --color-card-border:     #E0DBD2;
  --color-card-divider:    #E8E3DA;
  --color-tag-text:        #7A7268;
  /* One-off colors used inline: contact heading #E0DBD0, spotify link #4b4b4b,
     footer logo #5A5550, footer copy #4A4540 */

  /* Buttons (reference structural colors) */
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
```

---

## Fonts

Loaded from Google Fonts (single `<link>` in `<head>`):
- **Cormorant Garamond** — weights 300, 400
- **DM Sans** — weights 300, 400, 500
- **DM Mono** — weights 300, 400, 500

---

## HTML Structure

```html
<body>
  <section id="hero">
    <header>...</header>       <!-- nav overlay -->
    <!-- portrait div -->
    <!-- gradient overlays (4 divs) -->
    <!-- hero content -->
  </section>
  <section id="ticker">...</section>
  <section id="what-i-offer">...</section>
  <section id="performances">...</section>
  <section id="contact">...</section>
  <footer>...</footer>
</body>
```

---

## Section Specs

### 1. Nav (inside Hero, absolutely positioned)
- Height: 64px, full width
- Layout: flexbox, `justify-content: space-between`, `align-items: center`
- Padding: `0 var(--padding-nav-x)`
- **Left:** "ADAM GUO" — DM Sans 13px, weight 500, letter-spacing 6px
- **Right:** links "WHAT I OFFER" | "PERFORMANCES" | "CONTACT" — DM Sans 12px, weight 300, letter-spacing 1px, gap `var(--gap-nav-links)`
- Links are `<a href="#what-i-offer">` etc. for smooth scroll

### 2. Hero
- Background: `var(--color-cream)`
- Height: 720px, `overflow: hidden`, `position: relative`
- **Portrait:** absolutely positioned div, width 741px, height 720px, right 0, top 0 — `background-image: url(images/portrait.png)`, `background-size: cover`
- **Gradient overlays:** 4 absolutely positioned divs on top of portrait, each a linear-gradient from `#F7F4EE` to transparent (top, right, bottom, left directions) to blend photo into background
- **Content (left):** `position: relative; z-index: 1`, padding `160px var(--padding-section-x) 0` (160px clears the 64px nav + 96px breathing room), vertical flex, gap `var(--gap-hero-content)`
  - Eyebrow: "SOLOIST — CHAMBER MUSICIAN — RECORDING ARTIST" — DM Mono 10px, letter-spacing 3px, color `var(--color-text-muted)`
  - H1: "Hi, I'm Adam Guo" — Cormorant Garamond 96px, weight 300, line-height 0.93, max-width 443px
  - Body: 2-paragraph bio — DM Sans 15px, weight 300, line-height 1.7, max-width 520px, color `var(--color-text-secondary)`
  - CTA row (flex, gap `var(--gap-hero-cta)`):
    - "Contact" button — `var(--btn-primary-bg)` bg, `var(--btn-primary-text)` text, padding `var(--padding-btn-primary)`, DM Sans 10px weight 500, letter-spacing 2px, no border-radius
    - "Listen on Spotify →" link — DM Mono 12px, weight 300, letter-spacing 0.5px, color `#4b4b4b`

### 3. Trust Ticker
- Background: `var(--color-dark)`
- Height: 52px, full width
- Layout: flexbox, `justify-content: space-between`, `align-items: center`
- Padding: `0 var(--padding-nav-x)`
- 5 credential pairs separated by 1px × 10px white vertical dividers
- Each pair: primary label (DM Mono 10px, weight 500, letter-spacing 2px, color `var(--color-text-faint)`) + secondary label (DM Mono 10px, color `var(--color-tag-text)`)
- Items: "NEW SCHOOL / ALUMNI '25", "EAST BRUNSWICK SYMPHONY ORCHESTRA / VIOLINIST", "STUDIO OF MICHELLE KIM", "B.M.M.M", "MUSICIAN"

### 4. What I Offer
- Background: `var(--color-cream)`
- Padding: `var(--padding-section-y) var(--padding-section-x)`
- Vertical flex, gap 32px
- **Label row:** "WHAT I OFFER" — DM Mono 10px, weight 500, letter-spacing 3px, color `var(--color-text-muted)`
- **Pillars grid:** horizontal flex, background `var(--color-separator)`, gap `var(--gap-pillars-grid)` — creates hairline separator between cards
  - 3 cards, each `flex: 1`, background `var(--color-cream)`, padding `var(--padding-pillar-card)`, vertical flex, gap 12px
  - Number: DM Mono 10px, weight 300, letter-spacing 1px, color `var(--color-text-faint)`
  - Title: Cormorant Garamond 26px — corrected to "Violin **Lessons**" (typo fix)
  - Body: DM Sans 12px, weight 300, line-height 1.7, color `var(--color-text-muted)`

### 5. Featured Performances
- Background: `var(--color-warm-gray)`
- Padding: `var(--padding-section-y) var(--padding-section-x)`
- Vertical flex, gap 40px
- **Header row:** "Featured Performances" — Cormorant Garamond 32px, weight 300
- **Cards grid:** horizontal flex, gap `var(--gap-cards-grid)`
  - 3 cards, each `flex: 1`, border `1px solid var(--color-card-border)`, background `var(--color-cream)`
  - Image area: 180px height, `background-size: cover`, `background-position: center`
  - Divider: 1px `var(--color-card-divider)`
  - Body: padding `var(--padding-card-body)`, vertical flex, gap 12px
    - Platform label: DM Sans 11px, weight 500, letter-spacing 0.5px
    - Chip row: flex, gap 6px — each chip: DM Mono 8px, color `var(--color-tag-text)`, border `1px solid var(--color-card-border)`, padding `var(--padding-chip)`
    - Status: DM Mono 9px, letter-spacing 1.5px, color `var(--color-text-muted)`

### 6. Contact
- Background: `var(--color-dark)`
- Padding: `88px var(--padding-section-x)`
- Layout: horizontal flex, gap `var(--gap-contact)`, `align-items: flex-start`

**Left column (width: 480px, vertical flex, `justify-content: space-between`):**
- "GET IN TOUCH" — DM Mono 9px, weight 500, letter-spacing 3px, color white
- "Contact:" heading — Cormorant Garamond 52px, weight 300, line-height 1.05, color `#E0DBD0`
- Email + phone — DM Mono 24px, weight 300, color `var(--color-text-faint)`
- Body copy — DM Sans 14px, line-height 1.7, color `var(--color-tag-text)`, max-width 400px
- Social links row (flex, gap `var(--gap-social-links)`):
  - Each link: flex, gap 6px, icon (Lucide 14×14, color `var(--color-tag-text)`) + label (DM Mono 11px, weight 300, letter-spacing 1px)
  - Links: Instagram, Spotify, YouTube

**Right column (flex: 1, vertical flex, gap `var(--gap-form-fields)`):**
- `<form action="https://api.web3forms.com/submit" method="POST">`
- `<input type="hidden" name="access_key" value="YOUR_ACCESS_KEY">`
- Name row: horizontal flex, gap `var(--gap-form-name-row)` — First Name + Last Name inputs (each `flex: 1`)
- Email input
- Subject input
- Message `<textarea>` height 120px
- Submit `<button type="submit">SEND MESSAGE</button>` — full width, `var(--btn-submit-bg)` bg, `var(--btn-submit-text)` text, padding `var(--padding-btn-submit)`, DM Sans 11px, weight 500, letter-spacing 2px, no border-radius
- All inputs: background `var(--color-input-bg)`, border `1px solid var(--color-input-border)`, `border-radius: 6px`, padding `var(--padding-input)`, color `var(--color-text-faint)`, DM Sans 13px
- Labels: DM Sans 12px, weight 500, color `var(--color-text-faint)`

### 7. Footer
- Background: `var(--color-dark)`
- Height: 64px, full width
- Layout: flexbox, `justify-content: space-between`, `align-items: center`
- Padding: `0 var(--padding-footer-x)`
- Left: "ADAM GUO" — DM Sans 11px, weight 500, letter-spacing 5px, color `#5A5550`
- Right: "© 2026 Adam Guo. All rights reserved." — DM Mono 9px, weight 300, letter-spacing 1px, color `#4A4540`

---

## Icons

Lucide via CDN in `<head>`:
```html
<script src="https://unpkg.com/lucide@latest"></script>
```
Initialize at bottom of `<body>`:
```html
<script>lucide.createIcons();</script>
```
Usage: `<i data-lucide="instagram"></i>`

---

## Web3Forms Integration

- Form `action="https://api.web3forms.com/submit"` + `method="POST"`
- Hidden input: `<input type="hidden" name="access_key" value="YOUR_KEY">`
- Adam signs up at web3forms.com, gets key, replaces `YOUR_KEY`
- All fields have `name` attributes so Web3Forms can label them in the email

---

## Performance Card Images

Pulled from external URLs — no local files needed:

| Card | Platform | Image URL |
|---|---|---|
| 1 | YouTube | `https://img.youtube.com/vi/HU9k3WdWd6I/maxresdefault.jpg` |
| 2 | YouTube | `https://img.youtube.com/vi/IN5kOooVeF8/maxresdefault.jpg` |
| 3 | Spotify | `https://i.scdn.co/image/ab67616d00001e02ea57896b4f072641ad3fccf7` |

Card chips ("Solo Recital", "Baroque", etc.) are placeholder text — to be updated once links are finalized.

---

## Responsive Breakpoints

Single breakpoint at **768px**. Above: desktop layout. Below: everything stacks.

### Changes at ≤ 768px

**Nav:**
- Switch from `flex-direction: row` to `flex-direction: column`
- Center both logo and links
- Reduce padding to `16px`

**Hero:**
- Portrait div hidden (`display: none`)
- Content goes full width, padding reduced to `24px`
- H1 font size drops from 96px → 48px
- Gradient overlays hidden (no portrait to blend)

**Trust Ticker:**
- Switch to auto-scrolling marquee via CSS animation
- Duplicate all ticker items in HTML (2 full sets back-to-back)
- Animate `transform: translateX(-50%)` on a continuous loop — seamless because both sets are identical
- Dividers visible (they scroll with the content)
- `overflow: hidden` on the container to clip the scrolling track
- Desktop keeps the static `justify-content: space-between` layout; mobile switches to the scrolling version

**What I Offer (pillars):**
- Grid switches from `flex-direction: row` → `flex-direction: column`
- `gap` replaces the 1px separator background trick (use `border-bottom` on each card instead)

**Featured Performances (cards):**
- Grid switches from `flex-direction: row` → `flex-direction: column`
- Each card goes full width

**Contact:**
- Switch from `flex-direction: row` → `flex-direction: column`
- Left column goes full width
- Form goes full width
- Reduce padding to `48px 24px`

**Footer:**
- Switch to `flex-direction: column`, `gap: 8px`, `text-align: center`
- Reduce padding to `16px`

---

## Known Fixes from Design

- "Violin Lessions" → corrected to "Violin Lessons" in code
- Hero portrait filename is a Google CDN URL in design — replaced with local `images/portrait.png`
- Performance card images (`generated-*.png`) → replaced with local `images/performance-1.png` etc.
