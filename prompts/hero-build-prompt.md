# Build Prompt: Boardy Pro Hero

Hand this to a coding agent. It is self-contained, but the canonical source of truth is [`boardy-pro-research/06-hero-spec.md`](../boardy-pro-research/06-hero-spec.md). If anything here conflicts with that spec, the spec wins. Also read [`CLAUDE.md`](../CLAUDE.md) for the hard rules before starting.

---

## Goal

Build the **hero section** for the Boardy Pro landing page: a brushed-brass Boardy standing center-stage in a warm-white spotlight, an oversized brass "PRO" forged behind him, on a cool near-black stage, with an inline phone-number field as the conversion action. Pixel-quality, production-ready, responsive, accessible. This is a launch-moment hero, so it should feel premium and confident, not like a generic SaaS template.

Build the hero only. Leave clean seams so the rest of the page (see `07-section-flow.md`) can be added below it later.

## Tech stack (decided)

- **Next.js (App Router) + TypeScript + Tailwind CSS.** This is the chosen stack, not a suggestion. If the repo has no app yet, scaffold it. Deploy target is Vercel.
- Single hero component, e.g. `components/Hero.tsx`, rendered on the home route.
- Define the design tokens as CSS variables (in `globals.css`) and/or `tailwind.config` theme extensions so the rest of the page reuses them.
- No heavy animation libraries needed. Plain CSS keyframes and transitions are enough. Framer Motion is acceptable if it stays lightweight.

## Asset

- Character image: `golden boardy pro.png` (repo root). Brushed-brass box head, blue Boardy face, navy suit, red tie, chest-cropped, transparent background. Move it into the app's public assets dir and reference it. Do not recolor or regenerate it.

## Design tokens (use exactly)

```
/* Background (cool dark stage) */
--bg-base:        #0B0E14;  /* hero base */
--bg-radial-top:  #141A26;  /* faint top-center lift behind PRO */

/* Spotlight (warm white, NOT peach, NOT saturated) */
--spot-core:      #FCF6EA;  /* hottest, directly behind Boardy */
--spot-mid:       #EBD9B4;  /* soft gold-tinted falloff */
/* falls off to transparent toward the sides */

/* Brass (character + PRO + arc keyline) */
--brass-highlight:#E8C98A;
--brass-mid:      #C99A4B;
--brass-shadow:   #8A6A2E;

/* Boardy blue (interactive only) */
--boardy-blue:      #2D7DD2;
--boardy-blue-hover:#246BB8;

/* Text + field */
--text-primary:   #F5F3EE;  /* headline, warm off-white */
--text-secondary: #A8B0BD;  /* subhead */
--text-offer:     #E8C98A;  /* offer microcopy, brass */
--field-bg:       #161B24;
--field-border:   #2A3340;  /* focus -> --boardy-blue */
--accent-red:     #B23A2E;  /* tiny accents only */
```

**Color rules:** brass is the character, PRO, and arc keyline. Blue is for anything clickable only. Cool dark stage, warm-white spotlight. No third brand color. The background must stay cool. A warm background mutes the brass and kills the whole effect.

## Typography

- Display grotesk, heavy. Use **Space Grotesk** (or Archivo) via `next/font` or Google Fonts. Body can be the same family or Inter.
- Headline: clamp ~64-80px desktop, ~36-40px mobile, weight 700, color `--text-primary`, line-height ~1.05, two lines.
- Subhead: 20-22px, weight 400, `--text-secondary`, max-width ~540px, centered.
- PRO backdrop: enormous, ~36-44vw, weight 800-900, brass gradient fill, low contrast.
- Field text 18px; button label 17-18px weight 600; offer microcopy 14-15px.

## Exact copy (do not paraphrase)

- Headline (two lines):
  - "I'm done making intros."
  - "Now I make deals happen."
- Subhead: "I pressure-test the fit, sit in on the calls, and chase the follow-ups so the deal actually closes. You take the win."
- Phone field placeholder: "Your phone number"
- Submit button: "Talk to Boardy"
- Offer line (under field): "Free for your first year."
- Reassurance line (tiny, under offer): "I'll call you. No spam, no forms."

No em dashes anywhere.

## Layout: centered monument

Full-viewport hero (`min-height: 100vh`), single centered column on the vertical axis.

Stacking order, back to front:
1. Cool radial background (`--bg-radial-top` upper center fading to `--bg-base`).
2. **PRO** brass wordmark, huge, centered, low contrast (~0.5 opacity against bg). Behind the character.
3. **The arc**: warm-white spotlight glow + crisp curved edge + brass keyline, seated at the bottom region.
4. **Brass Boardy** character, centered, upper-middle, standing on the arc apex, overlapping and occluding part of the PRO letters so character and type read as one object.
5. Text column below the character: headline -> subhead -> phone field row -> offer line -> reassurance line.

The character's chest crop should sit near the arc line so the spotlight softens the transition. He reads as standing in light, not pasted on.

## The arc (the signature element, get this right)

Three jobs at once: a horizon, a stage lip, and the source of the spotlight. Build it with SVG + CSS, no raster.

- **Shape:** a shallow convex curve. The cool dark stage's bottom edge bulges gently downward, apex centered under Boardy. Span the full hero width. Rise from the side baseline to the center apex is small, roughly 4-8% of hero height. Keep it shallow and wide so it reads as a confident horizon, not a deep bowl or a smile. Implement as a single quadratic-bezier SVG path (flat at the sides, control point raised at center) or a wide CSS ellipse.
- **Edge:** crisp line between the cool dark (above) and the warm-white spotlight zone (below/behind). No feathering of the edge itself.
- **Brass keyline:** a hairline stroke (~1.5-2px) riding the top of the curve, `--brass-highlight` into `--brass-mid`, with a soft brass glow bleeding a few px upward. This is the premium detail. It ties the horizon to the brass material.
- **Spotlight glow:** a warm-white radial (`--spot-core` -> `--spot-mid` -> transparent) centered at the apex, hottest directly behind Boardy, falling off toward the left and right edges so the sides of the arc sink into the dark. Pool it low and central. It must NOT wash up into the PRO word or flatten the cool background.
- **No brass spill** into the glow below the keyline. Keyline only, for now.

## PRO wordmark

- Live text with a CSS brass gradient (`--brass-highlight` top -> `--brass-shadow` bottom), so it stays crisp and responsive. SVG text is fine too.
- Low contrast, ~0.5 opacity against the background. It is a backdrop, not a competitor for attention.
- A faint top specular line sells the "forged metal" read.
- The character overlaps it. Attention order must be: brass Boardy first, then headline, then the phone field, then PRO.

## Phone field behavior

- A single centered row, max-width ~520px: `tel` input (flex-grow) + submit button. On mobile they stack full-width.
- Input: `--field-bg` fill, `--field-border` border, focus transitions border/ring to `--boardy-blue` with a soft glow.
- Include a country-code prefix or selector; default to the user locale.
- Light client-side validation (length/format) before enabling submit.
- Button: `--boardy-blue` fill, hover `--boardy-blue-hover`, label "Talk to Boardy", subtle blue glow so it lifts off the dark.
- On submit: stub a handler that would route into a phone-verify flow (mirrors onboarding.boardy.ai). Do NOT build an email/password signup. Leave a clear TODO and a typed `onSubmit(phone: string)` seam for wiring later.
- Offer line "Free for your first year." in brass directly beneath the field, then the tiny reassurance line.

## Motion (subtle life only)

Wrap all of this in a `prefers-reduced-motion: reduce` guard that disables it.

- **Boardy entrance:** on load, character eases up ~24px and fades in over ~700ms ease-out, like he rises into the spotlight. The spotlight glow brightens slightly in sync.
- **Brass shimmer:** a slow, low-opacity specular highlight sweeps across the box, the PRO letters, and the arc keyline on a long ~6-8s loop. Barely there.
- **Spotlight breathe:** very subtle opacity/scale oscillation on the warm-white glow, ~8s.
- **Field focus:** the border/glow transition described above.
- No parallax, no bounce, no looping character animation, nothing that pulls the eye off the headline or field.

## Responsive

- Desktop: full centered composition.
- Tablet: PRO scales down, headline clamps, character ~60% width, arc keeps proportions, field row stays horizontal if it fits else stacks.
- Mobile: tight stack. Character ~80% width centered, PRO crops at the edges behind it, headline ~36-40px, field + button stack full-width, offer + reassurance beneath. Arc flattens slightly but keeps the keyline.

## Accessibility

- Semantic landmarks: the hero in a `<section>`, one `<h1>` for the headline.
- The phone input has a real (visually-hidden if needed) `<label>`, `type="tel"`, `inputmode="tel"`, `autocomplete="tel"`.
- Visible focus states on input and button (the blue ring counts).
- The PNG has meaningful `alt` (e.g. "Boardy, the AI superconnector, in brushed brass").
- Color contrast: headline and body text must pass WCAG AA against the dark stage (the chosen text tokens do, keep it that way).
- Respect reduced motion as above.

## Definition of done

- Renders the hero exactly per layout, copy, and tokens above.
- The arc reads as a crisp shallow horizon with a brass keyline and a warm-white spotlight pooled behind Boardy. Not peach, not a deep bowl, not feathered at the edge.
- Brass Boardy overlaps the PRO letters and is the clear focal point.
- Inline phone field works (validates, shows focus state, calls a typed `onSubmit` stub). No email/password anywhere.
- Subtle motion present and fully disabled under reduced-motion.
- Responsive across desktop/tablet/mobile with no overflow or layout breakage.
- No em dashes in any rendered copy or code comments.
- Design tokens defined centrally and reused, ready for the rest of the page to consume.

## Deliverables

- The hero component + supporting styles/tokens, wired into the home route so it renders.
- Brief note in the PR/summary of any decisions made on the still-open items (typeface confirmation, exact arc curvature, keyline weight). If you change a design decision, update `boardy-pro-research/06-hero-spec.md` in the same change.
- A screenshot or short clip of the result if the environment can produce one.
