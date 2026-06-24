# Boardy Pro Hero: Build Spec (decisions locked)

Status: final hero spec. Decisions made in brainstorm:
- **Composition:** centered monument (PRO huge + centered, brass Boardy through it, headline clean below).
- **CTA mechanic:** inline phone field in the hero (phone-first, collapses funnel to one step).
- **Motion:** subtle life (Boardy eases out of the spotlight on load, slow brass shimmer, gentle glow breathe, no flash).
- **Headline:** "I'm done making intros. Now I make deals happen."
- **The arc:** shallow convex horizon at the base, crisp edge with a thin brass keyline, warm-white spotlight glowing behind Boardy. No brass spill (yet).
- **No eyebrow line.** Headline carries the framing.

Palette and type tokens carry forward to the rest of the page. See [07-section-flow.md](07-section-flow.md).

---

## 1. Concept

A launch-moment monument. The oversized brass word **PRO** is forged behind a brushed-brass Boardy who stands center-stage in a warm-white spotlight, cradled by a curved, brass-edged horizon (the arc) on a cool near-black stage. The headline delivers the connector-to-closer pivot in Boardy's own voice. The conversion action is a single inline phone field: drop your number, Boardy takes it from there. The free-first-year offer sits right beneath it.

**Attention order:** brass Boardy → headline → phone field → PRO backdrop.

---

## 2. Color palette

### Background (cool dark stage)
| Token | Hex | Use |
|---|---|---|
| `bg-base` | `#0B0E14` | Hero base, cool charcoal-black |
| `bg-radial-top` | `#141A26` | Faint top-center radial lift behind PRO |

Vertical/radial blend `#141A26` (upper center) to `#0B0E14` (edges). Keep cool. Warm bg kills the brass.

### Spotlight (warm white, the light Boardy stands in)
| Token | Hex | Use |
|---|---|---|
| `spot-core` | `#FCF6EA` | Hottest point, directly behind Boardy at the apex |
| `spot-mid` | `#EBD9B4` | Soft gold-tinted falloff |
| `spot-edge` | transparent | Fades to nothing into the dark toward the sides |

The spotlight is warm-white with a hint of gold, NOT peach and NOT saturated. It reads as theatrical light, keeps the brass clean, and lets Boardy be the only saturated thing in the frame. Hottest behind him, falling off to the sides. See the arc section for geometry.

### Brass (character + PRO + arc keyline, hero material)
| Token | Hex | Use |
|---|---|---|
| `brass-highlight` | `#E8C98A` | Specular highlights, top edge of PRO, arc keyline, offer microcopy |
| `brass-mid` | `#C99A4B` | Core brass tone |
| `brass-shadow` | `#8A6A2E` | Recesses, lower gradient of PRO |

### Boardy blue (the interactive color)
| Token | Hex | Use |
|---|---|---|
| `boardy-blue` | `#2D7DD2` | Phone-field submit button, links, focus ring |
| `boardy-blue-hover` | `#246BB8` | Hover |

Rule: **brass = character + arc. blue = anything clickable.** Button rhymes with his face. No third brand color.

### Text + accent
| Token | Hex | Use |
|---|---|---|
| `text-primary` | `#F5F3EE` | Headline, warm off-white |
| `text-secondary` | `#A8B0BD` | Subhead, cool muted grey |
| `text-offer` | `#E8C98A` | "Free for your first year" (brass) |
| `field-bg` | `#161B24` | Phone field fill |
| `field-border` | `#2A3340` | Phone field border (focus -> boardy-blue) |
| `accent-red` | `#B23A2E` | Tie-red. Tiny accents only |

---

## 3. Typography

Display grotesk, heavy. Recommended **Space Grotesk** or **Archivo** (free, bold, characterful, premium-but-playful). Body in the same family or Inter.

| Element | Size (desktop) | Weight | Color | Notes |
|---|---|---|---|---|
| `PRO` backdrop | 36-44vw | 800/900 | brass gradient | Behind character, low contrast (~0.5) |
| Headline | 64-80px (clamp) | 700 | `text-primary` | Two lines, leading ~1.05 |
| Subhead | 20-22px | 400 | `text-secondary` | Max ~540px, centered |
| Field input text | 18px | 500 | `text-primary` | |
| Submit button | 17-18px | 600 | white on blue | |
| Offer microcopy | 14-15px | 500 | `text-offer` | Under the field |

Mobile: headline clamps ~36-40px, PRO scales with viewport but stays behind character.

---

## 4. Copy (final)

- **Headline:** "I'm done making intros. Now I make deals happen."
  - Line break: "I'm done making intros." / "Now I make deals happen."
- **Subhead:** "I pressure-test the fit, sit in on the calls, and chase the follow-ups so the deal actually closes. You take the win."
- **Phone field placeholder:** "Your phone number"
- **Submit button:** "Talk to Boardy"
- **Offer line (under field):** "Free for your first year."
- **Reassurance microcopy (optional, tiny, under offer):** "I'll call you. No spam, no forms."

Voice: first person, Boardy speaking. No em dashes. Alternates in [03-voice-and-copy.md](03-voice-and-copy.md).

---

## 5. Layout (centered monument)

Full-viewport hero (`min-height: 100vh`), single centered column, everything on the vertical axis.

```
+--------------------------------------------------+
|   [nav: brass boardy mark]               [ Pro ] |
|                                                  |
|              P  R  O   (brass, behind)           |
|                  ___                             |
|                 |o o|   <- brass Boardy,         |
|                 | \_/|      blue face,           |
|                  \__/       rises on load        |
|                                                  |
|        I'm done making intros.                   |
|        Now I make deals happen.                  |
|                                                  |
|   I pressure-test the fit, sit in on the calls,  |
|   and chase the follow-ups so the deal closes.   |
|                                                  |
|     [ Your phone number      ] [ Talk to Boardy ]|
|              Free for your first year.           |
|   __________ warm-white spotlight ___________    |
|  /          (crisp arc + brass keyline)       \  |
+--------------------------------------------------+
```

### Stacking order (back to front)
1. `bg-base` cool radial
2. `PRO` brass wordmark, low contrast, centered
3. The arc: warm-white spotlight glow + crisp curved edge + brass keyline (bottom region)
4. Brass Boardy character, centered, standing on the arc apex, overlapping the PRO counters
5. Text column: headline -> subhead -> phone field row -> offer line

### Character placement
- Optical center, upper-middle. Overlaps and occludes part of PRO so he's locked into the type (as in the mockup, box sitting in the PRO counter-space).
- He stands at the apex of the arc, lit by the spotlight. Chest crop (bottom of the PNG) sits just above or right at the arc line; the spotlight glow softens the transition so the hard crop edge reads as "standing in light," not "pasted on."

### Phone field row
- Single horizontal row, centered, max-width ~520px: input (flex-grow) + submit button.
- Field: `field-bg` fill, `field-border`, focus border/ring -> `boardy-blue`.
- Button: `boardy-blue`, "Talk to Boardy", subtle blue glow.
- On mobile: field and button stack full-width.

---

## 5b. The arc (horizon + spotlight)

The signature element. Three jobs at once: a horizon (Boardy stands on the world), a stage lip (center-stage), and the source of the spotlight.

### Geometry
- **Shallow convex curve.** The dark stage's bottom edge bulges gently downward, apex centered under Boardy. Keep it shallow and wide, a confident horizon, not a deep bowl or a swoosh/smile.
- Suggested proportions: arc spans full hero width; rise from edge to apex is small (roughly 4-8% of hero height). Tune by eye so it reads as a subtle horizon.
- Build as an SVG path (single quadratic bezier: baseline at the sides, control point raised at center) or a wide CSS ellipse. SVG path is cleaner and easier to keyline.

### Edge treatment (locked)
- **Crisp line** between the cool dark stage (above) and the warm-white spotlight zone (below/behind). No feathering of the edge itself.
- **Thin brass keyline riding the arc:** a hairline (~1.5-2px) in `brass-highlight` -> `brass-mid` along the top of the curve, with a soft brass glow bleeding upward a few px. This is the premium detail: it ties the horizon to the brass material and makes the curve intentional.
- **No brass spill** into the glow below the line yet (revisit later). The brass lives only in the keyline for now.

### The spotlight glow
- A warm-white radial (`spot-core` -> `spot-mid` -> transparent) seated at the apex, **hottest directly behind Boardy**, falling off toward the left and right edges so the sides of the arc sink back into the dark.
- The glow sits behind the character and just above/around the arc line, so he reads as standing IN the light, not in front of a colored band.
- Contain it: the glow should not wash up into the PRO word or flatten the cool background. It pools low and central.

---

## 6. Inline phone field behavior

- Input type `tel`, with a country-code prefix/selector if international (default to user locale).
- Light client validation (length/format) before enabling submit.
- Submit -> the boardy.ai phone-verify flow (mirrors onboarding.boardy.ai: verify number, then continue). Do not invent an email/password step.
- Offer line `Free for your first year.` in brass directly beneath.
- Tiny reassurance line under that: "I'll call you. No spam, no forms." (sets expectation that the next touch is a phone call, which is the actual product).

---

## 7. PRO word treatment

- Fill: vertical brass gradient `brass-highlight` (top) -> `brass-shadow` (bottom), same material as the box.
- Low contrast (~0.5 against bg): backdrop, not competitor.
- Faint top specular line sells "forged metal."
- Character overlaps the letters, occluding part of them, unifying type + character into one object.
- Build as live text with CSS gradient if possible (responsive, crisp), or supply a brass vector.

---

## 8. Motion spec (subtle life)

Keep it quiet and premium. Respect `prefers-reduced-motion` (disable all of the below if set).

- **Boardy entrance:** on load, character eases up ~24px and fades in over ~700ms, `ease-out`. Like he rises into the spotlight. The spotlight glow brightens slightly in sync.
- **Brass shimmer:** a slow, low-opacity specular highlight sweeps across the box, the PRO letters, and the arc keyline on a long loop (~6-8s), barely-there. Sells the metal.
- **Spotlight breathe:** very subtle opacity/scale oscillation on the warm-white glow (~8s) so the light feels alive, not painted.
- **Field focus:** border transitions to `boardy-blue` with a soft glow on focus.
- **No:** parallax jank, bouncing, looping character animation, anything that pulls focus from the headline/field.

---

## 9. Navigation (top of hero)

Minimal. Left: small brass Boardy mark + "Pro" lockup. Right: optional single text link (e.g. "How it works" anchor) and nothing else, or leave it bare. The conversion is the hero field, so the nav stays out of the way. Transparent over the dark hero.

---

## 10. Responsive

- Desktop: full centered composition as above.
- Tablet: PRO scales down, headline clamps, character ~60% width, arc keeps its proportions, field row stays horizontal if it fits else stacks.
- Mobile: tight stack. Character ~80% width centered, PRO crops at edges behind it, headline ~36-40px, field + button stack full-width, offer + reassurance beneath. Arc flattens slightly but keeps the keyline.

---

## 11. Assets

- Character: `golden boardy pro.png` (brushed brass box, blue face, navy suit, red tie, chest-cropped, transparent bg). Lives in the parent `Boardy Pro/` folder.
- `PRO` wordmark: build as live CSS-gradient text, or supply brass vector.
- Arc: build as SVG path + radial-gradient glow + brass keyline stroke. No raster needed.
- Fonts: Space Grotesk / Archivo (self-host or Google Fonts).

---

## 12. Don'ts

- No warm/orange background. Cool dark only, or the brass dies.
- Spotlight is warm-white, not peach, not saturated. Keep it subtle.
- No third brand color. Brass + blue + (tiny) red is the whole system.
- No em dashes.
- No brass spill into the glow yet. Keyline only.
- Don't let PRO out-contrast the character.
- Don't let the spotlight wash up into PRO or flatten the background.
- Don't add an email/password signup. Phone-first only.
- Don't over-animate. If motion draws the eye away from headline or field, cut it.
