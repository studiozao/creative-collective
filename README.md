# East Sussex Creative Collective — landing page

A single-page static site for the East Sussex Creative Collective, a free
programme for creative businesses across East Sussex, delivered by Studio Zao in
partnership with East Sussex County Council.

No frameworks, no build step. Plain HTML, CSS and vanilla JS.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Page structure and copy |
| `styles.css` | All styling, brand tokens, responsive rules, motion |
| `script.js` | Scroll reveals, hero parallax, connector animation, nav, analytics event |
| `README.md` | This file |

## Running it

- **Simplest:** double-click `index.html` to open it in a browser.
- **Recommended (so fonts/analytics behave):** run a tiny local server from this
  folder:
  ```bash
  python3 -m http.server 8000
  # then visit http://localhost:8000
  ```

## Before you launch — swap list

Every item below is marked in the code with `<<< SWAP >>>` so you can find it
fast (Cmd/Ctrl+F).

1. **Logos** — replace the two `STUDIO ZAO LOGO` / `ESCC LOGO` placeholder boxes
   in `index.html` (they appear in both the header and footer). Drop real files
   into an `assets/` folder and swap each placeholder `<span>` for something like:
   ```html
   <img src="assets/studio-zao-logo.svg" alt="Studio Zao" class="logo-img">
   ```
   Keep both logos on white, keep the thin `#D1D5DB` vertical rule between them.
   Suggested display size: ~40px tall (export at 2× for retina). The `.logo-img`
   class is already defined.

2. **Hero images** — the collage currently uses colour-gradient placeholders.
   In `styles.css` find the `.img-hands`, `.img-screen`, `.img-music`,
   `.img-market` (and optional `.img-film`, `.img-craft`) rules and replace
   `background-image` with your photos, e.g.
   `background-image: url("assets/hands.jpg");`. Briefed subjects are on each
   figure's `aria-label` in `index.html`. Suggested export: ~800×1000px,
   under 200KB each. The grid is built to look intentional with **4** images and
   expands to **6** — uncomment tiles 5 & 6 in `index.html` if you have them.

3. **Google Form URL** — in `index.html`, find the CTA button in the form
   section (`href="https://forms.gle/REPLACE_WITH_REAL_FORM_URL"`) and paste the
   real link. We deliberately do **not** iframe-embed the form — a native embed
   can't be restyled to match the brand, so a clean outbound button is correct.
   The hero and nav buttons scroll to this section.

4. **Analytics tracking ID** — in the `<head>` of `index.html` there are two
   pre-wired, commented-out snippets: **Plausible** (simplest) and
   **Google Analytics 4**. Uncomment ONE, add your ID/domain, delete the other.
   A custom CTA-click event (separate from the page view) fires automatically
   from `script.js` → `trackCtaClick()` and works with either provider.

5. **Eligibility copy — CONFIRM** — the eligibility checklist is a
   **placeholder** pending confirmation against the official programme spec.
   Review the three items in the Eligibility section of `index.html` before
   launch.

6. **Hack dates** — the form section is currently framed as an *expression of
   interest*, not a live booking, because Hack dates aren't confirmed. Once
   dates are live, update the copy in the form section (and the small microcopy
   line beneath the button), and swap the outbound button for a booking link if
   you move to live booking. This is flagged in `index.html`.

## Brand system (as implemented)

Colours are used exactly as specified (defined as CSS variables at the top of
`styles.css`):

| Token | Value | Use |
| --- | --- | --- |
| `--white` | `#FFFFFF` | Background |
| `--black` | `#000000` | Primary heading & body text |
| `--navy` | `#122D54` | Headings, nav, structural colour |
| `--grey` | `#6B7280` | Secondary text, labels, bullet dots |
| `--light-grey` | `#D1D5DB` | Dividers, cards, section bands |
| `--darker-grey` | `#4B5563` | Hover states, longer body text |
| `--red` | `#e42544` | CTA buttons + sparing highlights |

> Note: `--red-hover` (`#c51d38`) is a slightly darker red derived for button
> hover so white button text keeps AA contrast. If you'd rather not have a
> derived shade, change it in `styles.css`.

### Typography

- **Display / headings:** Space Grotesk
- **Body:** Inter
- Both loaded from Google Fonts in the `<head>`.

If the real Studio Zao typeface becomes available, swap the `<link>` in the
`<head>` and update `--font-display` / `--font-body` in `styles.css`.
Alternative confident sans pairings that work with this layout: *Sora + Inter*,
*Familjen Grotesk + Inter*, or *Archivo + IBM Plex Sans*.

## Accessibility & motion

- Semantic HTML, correct heading order, alt text / `aria-label` on all imagery.
- Keyboard navigable, visible focus rings, skip-to-content link.
- Colour contrast checked (navy and darker-grey used for body text on light
  bands where plain grey would fail; white-on-red CTA passes AA at ≈4.5:1).
- All animation respects `prefers-reduced-motion` — spatial motion collapses to
  a quick fade and looping animations are disabled.

## Notes on structure

The page is a continuous, immersive scroll (Apple-product-page spirit): generous
spacing between sections, soft white↔light-grey gradient bleed between bands,
content revealing on entry, subtle hero parallax, and a connector line that
draws in through "How it works". Scroll-snap was deliberately **not** used — in
testing it fought natural scrolling; the smooth continuous flow reads better.
