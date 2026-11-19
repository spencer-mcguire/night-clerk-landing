---
name: Night Clerk Cans
description: A staffed motel door at night — full-bleed plate, real logo as plaque, pill dock below.
colors:
  brown-950: "#1d100a"
  brown-900: "#2b1a12"
  cream: "#f7ead0"
  mustard: "#f2c14e"
  red: "#c1272d"
typography:
  body:
    fontFamily: "Archivo, system-ui, -apple-system, 'Segoe UI', sans-serif"
  social-pill:
    fontFamily: "Archivo, system-ui, -apple-system, 'Segoe UI', sans-serif"
    fontSize: "0.92rem"
    fontWeight: 700
    letterSpacing: "0.02em"
  fineprint:
    fontFamily: "Archivo, system-ui, -apple-system, 'Segoe UI', sans-serif"
    fontSize: "0.76rem"
    fontWeight: 600
    letterSpacing: "0.18em"
rounded:
  pill: "999px"
spacing:
  dock-bottom: "20px"
  dock-gap: "11px"
  pill-gap: "10px"
  pill-icon-gap: "9px"
  pill-padding: "10px 16px"
  fineprint-gap: "11px"
components:
  social-pill:
    backgroundColor: "rgba(29, 16, 10, 0.82)"
    textColor: "{colors.cream}"
    rounded: "{rounded.pill}"
    padding: "{spacing.pill-padding}"
  social-pill-hover:
    backgroundColor: "rgba(43, 26, 18, 0.96)"
    textColor: "{colors.cream}"
    rounded: "{rounded.pill}"
    padding: "{spacing.pill-padding}"
---

# Design System: Night Clerk Cans

## Overview

**Creative North Star: "The Staffed Door"**

The shipped page is not a centered logo on a solid ground. It is a full-bleed photographic motel door, ajar with warm light spilling out, covering the whole first viewport (`min-height: 100dvh`). The supplied logo lockup is mounted on that door as its plaque, and a single pill dock sits bottom-center. Nothing else competes: no headline in web type, no card, no form. The visitor reads the brand, reads "Coming Soon" from the door hanger inside the plate, and follows a social or contact pill.

Archivo carries all live web type, in medium through bold, over a five-color palette lifted from the logo itself. Text is scarce by design; the mark and the plate do the talking.

**Key Characteristics:**

- Full-bleed door plate (`object-fit: cover`, centered) as the only background; `brown-950` is the fallback ground behind it
- Real logo lockup as plaque — never redrawn, never typeset as a substitute
- One component family: cream-outlined social pills on translucent dark brown, docked bottom-center with a spaced-caps fineprint line
- Mustard is an accent of response (focus ring, hover border), red an accent of selection — neither floods a surface
- One slow warm-light "spill" animation over the plate's lit edge; everything else moves only on hover

## Colors

A five-color palette taken from the supplied logo: two dark browns, cream, mustard, and a single red. Dark brown is the structural ground, cream the only text color, mustard and red scarce accents.

### Primary

- **Deep Door Brown** (`brown-950`, #1d100a): Page and door fallback ground, translucent pill background (at 82–96% opacity), and the base for every shadow and text-shadow on the page.
- **Sign Brown** (`brown-900`, #2b1a12): Browser theme color (`theme-color` meta), near-opaque pill hover ground, and the logo's dark register.

### Secondary

- **Mustard** (`mustard`, #f2c14e): Accent of response only — the 3px focus-visible outline and the social-pill hover border (at 80% opacity). Also the logo JPG's ground, supplied in the artwork, not painted by CSS.

### Tertiary

- **Clerk Red** (`red`, #c1272d): Text-selection background (with cream text) and the red carried inside the logo and plate artwork (VACANCY tab, key fob, script rule). CSS spends it in exactly one place.

### Neutral

- **Plaque Cream** (`cream`, #f7ead0): The only live text color, the social-pill border (at 34% opacity), and the plaque/paper tone of the world. There is no gray and no pure white or black anywhere in the shipped CSS.

### Named Rules

**The Five-Color Rule.** Live CSS uses only `brown-950`, `brown-900`, `cream`, `mustard`, and `red`, plus alpha variants of them and one warm spill glow (`rgba(255, 205, 105, 0.18)`). A new surface introduces no new hue; it reuses these or an alpha of them.

**The Scarce Accent Rule.** Mustard and red appear only as response or inside supplied artwork — focus, hover border, selection. Neither is ever a background fill for a live surface.

## Typography

**Display Font:** None in live type. Display lettering ("NightClerk" script, "CANS" slab, the hanger's "Coming Soon") exists only inside the supplied logo lockup and the photographic plate.
**Body Font:** Archivo (weights 500, 600, 700 loaded from Google Fonts), with `system-ui, -apple-system, "Segoe UI", sans-serif` fallback.
**Label/Mono Font:** None; labels are Archivo in spaced uppercase.

**Character:** One grotesque family doing every live job at small sizes. Weight, case, and letter-spacing — not size contrast — separate the pill labels from the fineprint.

### Hierarchy

- **Body** (Archivo, inherited size and weight): Page default on `brown-950` with cream text. The shipped page sets no visible paragraph in it; it is the inherited base for any future copy.
- **Social pill label** (Archivo 700, 0.92rem, letter-spacing 0.02em; 0.85rem at ≤820px): The only call-to-action text — "Instagram", "X", "Email".
- **Fineprint** (Archivo 600, 0.76rem, letter-spacing 0.18em, uppercase): The copyright line under the pills, legible over photography only via layered brown text-shadow.

### Named Rules

**The Imagery-Carries-Display Rule.** No webfont headline is set on this page. If a future surface needs display type, it must be decided and documented then — this system does not canonize the plate's or logo's lettering as a type token.

## Layout

A single-viewport composition with three absolutely positioned layers inside a `position: relative` door section (`min-height: 100dvh`, `overflow: hidden`, `isolation: isolate`):

- **Plate (z-index 0):** absolute, inset 0. Image fills with `object-fit: cover`, `object-position: center`. A dedicated mobile crop (`assets/scene-door-mobile.jpg`) swaps in at ≤820px via `<picture>`; desktop uses `assets/scene-door.jpg`.
- **Plaque (z-index 2):** the real logo lockup, `left: 6%`, `top: 30%`, `width: min(44%, 620px)`.
- **Dock (z-index 5):** absolute, horizontally centered (`left: 50%`, `translateX(-50%)`), `bottom: 20px`, a centered column with 11px gap: social pill row above, fineprint below. Width is content-sized, capped at `calc(100vw - 28px)`.

A warm spill layer (`::after`, z-index 1) sits between plate and plaque.

**Breakpoint — 820px (the only one).** At ≤820px the plaque re-centers: `left: 50%`, `top: 7%`, `translateX(-50%)`, `width: min(76vw, 340px)`. The dock tightens (`bottom: 14px`, `width: calc(100vw - 24px)`), pills shrink (9px 12px padding, 0.85rem type, 42px minimum height, 17px icons, 8px gaps).

**Spacing rhythm.** Small, tight steps only: 9px icon-to-label, 10px between pills, 11px between dock rows, 20px dock-to-viewport-bottom. No larger spacing token exists in the shipped page.

## Elevation & Depth

Depth is photographic first: the plate supplies real door, light, and shadow. CSS adds three brown-tinted lifts, all derived from `brown-950`, plus one animated light effect. There is no gray shadow anywhere.

### Shadow Vocabulary

- **Plaque drop** (`drop-shadow(0 22px 30px rgba(29, 16, 10, 0.38))`): A filter drop-shadow following the lockup's own silhouette, seating the plaque on the door.
- **Pill lift** (`box-shadow: 0 10px 24px rgba(29, 16, 10, 0.30)`): Lifts each social pill off the plate.
- **Fineprint scrim** (`text-shadow: 0 1px 10px rgba(29, 16, 10, 0.9), 0 0 22px rgba(29, 16, 10, 0.65)`): Not elevation — a legibility scrim standing in for a background panel behind the fineprint.

### Named Rules

**The Brown Shadow Rule.** Every shadow, drop-shadow, and text-shadow is `brown-950` at an alpha. Never black, never gray, never a colored glow — except the spill below, which is light, not shadow.

**The Spill Rule.** One radial warm glow (`50% 65% at 91% 42%`, `rgba(255, 205, 105, 0.18)` fading to transparent at 62%) breathes over the plate's lit edge on a 5.5s ease-in-out infinite loop (opacity 0.65 → 1 with a 0.78/0.95 flicker at 52%/56%). It is the page's only ambient motion and the first thing reduced-motion removes.

## Shapes

One shape: the full pill (`border-radius: 999px`) — every social link and the focus-visible outline. No cards, panels, inputs, or rectangular buttons exist in the shipped page. Icon artwork inside pills is 19px inline SVG (17px at ≤820px), stroke-based at 2px with round caps for Instagram and Email, filled for X. The plaque and plate are unclipped rectangles; their silhouettes come from the artwork itself.

## Components

### Social Pill (the only interactive component)

Cream text on translucent door-brown, outlined in cream, fully rounded — built to sit over photography.

- **Shape:** Full pill (999px), `min-height: 44px` (42px at ≤820px), inline-flex with 9px icon-to-label gap.
- **Default:** Background `rgba(29, 16, 10, 0.82)`, text cream, 1.5px border `rgba(247, 234, 208, 0.34)`, padding 10px 16px, Archivo 700 at 0.92rem, pill lift shadow.
- **Hover:** Background deepens to `rgba(43, 26, 18, 0.96)`, border warms to `rgba(242, 193, 78, 0.8)` (mustard at 80%), `translateY(-1px)`. Transition 0.18s ease across background, transform, border-color.
- **Focus-visible (all links):** 3px solid mustard outline, 3px offset, 999px radius. Never removed.
- **Content rule:** Inline SVG icon + one-word label ("Instagram", "X", "Email"). Destinations are owner-supplied placeholders (`href="#"`, empty `mailto:`) until real URLs land — see Do's and Don'ts.

### The Plaque (signature component)

The supplied logo lockup (`assets/nightclerk-logo-lockup.png`, 1024×635) layered over the door plate — the real logo as a mounted motel sign, not a header logo.

- **Desktop:** `left: 6%`, `top: 30%`, `width: min(44%, 620px)`, plaque drop filter.
- **Mobile (≤820px):** Centered at top — `left: 50%`, `top: 7%`, `translateX(-50%)`, `width: min(76vw, 340px)`.
- **Rule:** The artwork is binding (see PRODUCT.md Brand Commitments). It is never redrawn, re-typeset, cropped by CSS, or placed on a CSS-painted panel.

### The Dock (signature component)

Bottom-center footer stack: social pill row (flex, wrap, centered, 10px gap) above the spaced-caps cream fineprint ("© 2026 Night Clerk Cans"). Absolute, `bottom: 20px` (14px mobile), z-index 5 — always above plate and spill, clear of the plaque at both breakpoint positions.

### The Door Plate

Full-bleed photographic background with its own warm spill overlay. Desktop and mobile crops are separate supplied rasters; alt text carries the scene description ("motel door ajar, warm light spilling out, brass knob with red diamond room key, door hanger reading Coming Soon — Quiet Hours, Every Hour"). The page's only heading is visually hidden (`sr-only` h1 carrying name, "Coming Soon", and tagline).

## Do's and Don'ts

### Do:

- **Do** build first viewports as a full-bleed plate with the real logo mounted on it — plaque at `left: 6% / top: 30% / min(44%, 620px)` desktop, centered `top: 7% / min(76vw, 340px)` at ≤820px.
- **Do** reuse the five tokens and their alphas only (`brown-950`, `brown-900`, `cream`, `mustard`, `red`); keep mustard to focus/hover response and red to selection and artwork.
- **Do** set live type in Archivo 500–700, cream on brown, with weight, case, and letter-spacing doing the separation work.
- **Do** keep touch targets at 44px minimum height and the focus state as the 3px mustard outline at 3px offset.
- **Do** honor `prefers-reduced-motion`: kill the spill animation and pill transitions, exactly as shipped.
- **Do** derive every shadow from `brown-950` at an alpha.

### Don't:

- **Don't** redraw, re-typeset, or substitute the logo lockup, and don't float it on a solid-color panel or card.
- **Don't** add a centered-logo-on-solid splash, a headline in web type, or any component family beyond the pill without documenting a system change here first.
- **Don't** introduce gray, pure black/white, or a sixth hue for UI chrome.
- **Don't** remove or restyle the mustard focus outline, and don't animate anything ambient besides the single spill — and never under reduced motion.
- **Don't** ship placeholder social destinations (`href="#"`, empty `mailto:`) as if they were final; they are owner-replaceable stubs, not a design decision.
