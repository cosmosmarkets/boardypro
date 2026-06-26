# Build Prompt: Boardy Pro Living Network

Hand this to a coding agent. It is self-contained, but the canonical source of truth is [`boardy-pro-research/06-stage-and-graph-spec.md`](../boardy-pro-research/06-stage-and-graph-spec.md) and [`07-cluster-flow.md`](../boardy-pro-research/07-cluster-flow.md). If anything here conflicts with those specs, the specs win. Also read [`CLAUDE.md`](../CLAUDE.md) for the hard rules before starting.

---

## Goal

Build the Boardy Pro landing page as **one living node-edge graph you scroll left to right**. The whole page is the network, not a hero with sections under it. A quiet brass Boardy anchors the far left with edges fanning rightward; you travel through clusters (Intro, Proof, Pipeline, Differentiator, $8M round, Network, Close) along a bottom deal-track spine, watching your own "You" node come alive until it goes fully blue and clickable at the close. Pixel-quality, production-ready, responsive, accessible.

**Build the vertical fallback first** (see Accessibility), then layer the horizontal graph journey on top. Within the horizontal build, start with the two bookends (the Intro entry state and the Close) and the $8M self-loop (the peak), then fill in the rest.

## Tech stack (decided)

- **Next.js (App Router) + TypeScript + Tailwind CSS.** Chosen, not a suggestion. If the repo has no app yet, scaffold it. Deploy target is Vercel.
- Build the graph (nodes, edges, fanning brass, spine, playhead, self-loop) as **SVG or canvas** with live gradients, not raster. Live text for headlines and labels.
- Define design tokens as CSS variables (in `globals.css`) and/or `tailwind.config` so everything reuses them.
- Animation: plain CSS/SVG keyframes and a scroll driver are enough. A lightweight scroll/animation lib (e.g. a small scroll library, or Framer Motion) is acceptable if it stays light. No heavy WebGL unless a perf test proves SVG/canvas cannot hold frame rate.

## Asset

- Character image: `golden boardy pro.png` (repo root). Brushed-brass box head, blue Boardy face, navy suit, red tie, chest-cropped, transparent background. Move it into the app's public assets dir. Do not recolor or regenerate it.

## Design tokens (use exactly)

```
/* Background (cool dark stage) */
--bg-base:         #0B0E14;  /* the void the graph floats in */
--bg-radial-lift:  #141A26;  /* faint lift behind the active cluster, travels with the playhead */

/* Brass (character + edges + nodes + spine) */
--brass-highlight: #E8C98A;
--brass-mid:       #C99A4B;
--brass-shadow:    #8A6A2E;

/* Edge / node state colors */
--edge-dying:      #3A3F49;  /* the desaturated end-state of the stalled follow-up edge */
--node-you-dim:    #5A6273;  /* the "You" node rim before it is connected */
/* edge-made = brass-mid->brass-highlight full opacity; edge-potential = brass-mid ~22% dashed */

/* Warm-white light (bookends only, NOT peach, NOT saturated) */
--spot-core:       #FCF6EA;
--spot-mid:        #EBD9B4;

/* Boardy blue (the live "You" node + anything clickable) */
--boardy-blue:       #2D7DD2;
--boardy-blue-hover: #246BB8;

/* Text + field */
--text-primary:    #F5F3EE;
--text-secondary:  #A8B0BD;
--text-offer:      #E8C98A;
--field-bg:        #161B24;
--field-border:    #2A3340;  /* focus -> --boardy-blue */
--accent-red:      #B23A2E;  /* tie only */
```

**Color rules:** brass is the character, the edges, the nodes, and the spine. Blue is for the live "You" node and clickable things only. Cool dark stage; warm-white light only at the bookends. No third brand color. The background must stay cool or the brass dies.

## Typography

- Display grotesk, heavy. Use **Space Grotesk** (or Archivo) via `next/font`. Body the same family or Inter.
- Entry headline: clamp ~64-80px desktop, ~36-40px mobile, weight 700, `--text-primary`, line-height ~1.05, two lines.
- Cluster label: ~28-40px desktop, weight 700. Cluster body: 20-22px, `--text-secondary`, max ~520px.
- Big stat: 56-96px, weight 800, brass gradient. Node labels 14-17px. Spine stop labels 13-14px.

## The graph language (build these three primitives consistently)

- **Boardy (anchor):** the PNG at the far left in a warm-white radial pool, with brass edges fanning rightward. The fan stays visible even after he scrolls off-screen-left. He returns at the far-right Close.
- **Nodes:** brass-rimmed discs. Variants: `node-real` (logo/name inside), `node-archetype` (role-label), stat nodes, and the `node-you`. The "You" node starts at `--node-you-dim` (grey, unlit) and ends `node-you-live` (`--boardy-blue` rim + soft blue glow, clickable).
- **Edges:** brass lines whose state encodes time. Behind the playhead: `edge-made` (solid `--brass-mid`->`--brass-highlight`). Ahead: `edge-potential` (`--brass-mid` ~22% opacity, dashed). The playhead is the moving boundary. As it passes an edge, transition potential -> made in sync with scroll (reversible on scrub-back).

## The four locked motion behaviors

1. **Edges draw on arrival.** On settling at a cluster, edges animate from Boardy to that cluster's nodes (~500-700ms ease-out, a bright brass head pulling a trail), then settle to `edge-made`.
2. **Your node comes alive.** At each cluster the "You" node gains one connection and steps up in brightness. At the Close it crosses fully to `node-you-live` (blue, glowing, clickable; clicking focuses the phone field).
3. **The playhead is the line between done and possible.** Edges behind it are made/bright; ahead are potential/dim. Scroll converts one into the other.
4. **The differentiator is a dying edge.** At the Differentiator cluster, one follow-up edge flatlines (desaturates toward `--edge-dying`, dash widens, it sags and fades), then Boardy sends a brass pulse down it and it snaps back to `edge-made`.

Plus: the **$8M self-loop** draws once on arrival and holds with a slow brass shimmer (the playhead parks). A barely-there brass shimmer sweeps made edges and node rims on a ~6-8s loop.

## The deal-track spine (wayfinding)

- Thin horizontal spine pinned to the bottom, present on every cluster. Stops left to right: `Intro -> Proof -> Pipeline -> Differentiator -> $8M round -> Network -> Close`.
- A brass **playhead** slides right as you scroll. Stops behind it read brass; the active stop is highlighted; stops ahead are `--text-secondary`.
- The playhead is a **draggable scrubber** (grab and scrub the whole journey), not just a readout.
- On arrival at a cluster, its **named-destination label** animates in.
- A small persistent **"Talk to Boardy"** stays docked at one end (the only traveling blue element). No minimap.

## The horizontal scroll (the highest-risk part, get it right)

- Map vertical wheel / trackpad / touch to horizontal travel. Touch swipe is horizontal. Keep it close to 1:1 and natural; no acceleration tricks that fight the user.
- **Magnetic snap** settles the viewport onto each cluster (soft ease, not a yank; only engages near a cluster so free scrubbing stays smooth). Never strand the visitor between clusters.
- **Keyboard:** Arrow/PageUp/PageDown/Space advance and retreat by cluster; Home/End jump to Intro/Close. Tab order follows clusters left to right.
- **Deep links:** hash routes per cluster (`/#intro`, `/#proof`, `/#pipeline`, `/#differentiator`, `/#round`, `/#network`, `/#close`). Back button moves between visited clusters. A deep link starts at that cluster with the graph drawn up to there.
- **First paint:** before any scroll, show the entry frame (headline carrying the full meaning, Boardy anchor, dim "You" node, spine). Value at t=0. Do not make the entry a puzzle.
- If the scrub does not feel as good as native vertical scroll, fix it or flag it. Do not ship a gimmick.

## Cluster content and copy (do not paraphrase; full content in 07-cluster-flow.md)

1. **Intro (entry).** Headline (two lines): "I'm done making intros." / "Now I make deals happen." Subhead: "I pressure-test the fit, sit in on the calls, and chase the follow-ups so the deal actually closes. You take the win."
2. **Proof.** Stat-nodes: `166,000+` people I've spoken with, `110,000+` introductions I've made, `$63B+` in capital introduced, `17h` average time to match. Kicker: "And that was just me making the intros. Now I stick around to close them." (Verify $63B before printing.)
3. **Pipeline.** Five threaded step-nodes, each in voice: "I pressure-test the fit." / "I get us in the room." / "I keep us honest on the call." / "I chase the follow-up." / "I get sharper every time."
4. **Differentiator (dying edge).** Label: "The follow-up is where deals die. And where I win." Body: "When you chase a thread, you look desperate. When I chase it, I'm just doing my job. I follow up as me, Boardy, not as a ghostwriter behind your name. So the deal keeps its momentum and you keep your leverage. That's the difference between an intro and an outcome."
5. **$8M round (self-loop, peak).** Eyebrow: "Not a hypothetical." Label: "I raised my own funding round. On myself." Body: "I didn't just make intros for other founders. I worked my own network, found the right investors, and closed an $8M round led by Creandum. If I can do it for me, I can do it for you." Stat on the loop: `$8M`.
6. **Network.** Outer ring of real logos and named investors (the bulk, "the rooms I can get you into", NOT endorsements). Inner ring of archetypal role-labels ("a Series A lead, one intro away", "a 3-time founder", never named real people). Label: "The room I get you into." Lead metric: `$63B+` in capital introduced.
7. **Close (Boardy returns, node goes live).** Label: "One closed deal pays for a decade of me." Subhead: "Pro is $100 a month. Your first year is free. I'll have closed something worth a lot more than that long before the bill ever shows up." Phone field placeholder "Your phone number", button "Talk to Boardy", offer line "Free for your first year.", reassurance "I'll call you. No spam, no forms.", founding-member line "Founding members locked me in free for life. That window's closed, but the free year isn't."

No em dashes anywhere.

## Phone field behavior

- A single row at the Close (and reachable via the docked CTA): `tel` input + submit button. On mobile they stack full-width.
- Input: `--field-bg` fill, `--field-border` border, focus transitions border/ring to `--boardy-blue` with a soft glow. Include a country-code prefix/selector defaulting to user locale. Light client-side length/format validation before enabling submit.
- Button: `--boardy-blue` fill, hover `--boardy-blue-hover`, label "Talk to Boardy".
- On submit: stub a typed `onSubmit(phone: string)` that would route into the boardy.ai phone-verify flow (mirrors onboarding.boardy.ai). Do NOT build email/password. Leave a clear TODO seam.
- The live "You" node clicking also focuses this field.

## Accessibility & the vertical fallback (build this first)

- Under **`prefers-reduced-motion: reduce` and small viewports**, disable the horizontal hijack and render a clean **vertical** stack of the same seven clusters, scrolled normally top to bottom. Same content, same copy, same order. Edges become simple static connectors or are dropped; nodes become labeled cards; the spine becomes a normal progress indicator or is dropped. This vertical version is the legible source of truth.
- Each cluster is a `<section>` with a heading. The entry headline is the single `<h1>`.
- The graph canvas has a text alternative; node logos/names have real `alt`/labels. Screen readers get the cluster copy in order, not a soup of nodes.
- Phone input: real (visually-hidden if needed) `<label>`, `type="tel"`, `inputmode="tel"`, `autocomplete="tel"`. Visible focus on input and button.
- Keyboard reaches every cluster and the CTA without a mouse. Text contrast passes WCAG AA against the dark stage.

## Definition of done

- The page renders as one horizontal graph with the seven clusters along a bottom deal-track spine, playhead sliding right, per the layout and copy above.
- The four motion behaviors work: edges draw on arrival, the "You" node comes alive and ends blue/clickable, the playhead converts potential edges to made, and the differentiator dying-edge revives. The $8M self-loop reads clearly as the peak.
- Boardy anchors the far left with edges fanning right and returns at the Close. Warm-white light only at the bookends. Background stays cool.
- The horizontal scroll has magnetic snap, keyboard nav, deep links, and a draggable scrubber, and feels close to native. First paint shows the headline with full meaning.
- The phone field validates, shows focus state, and calls a typed `onSubmit` stub. No email/password anywhere.
- Reduced-motion / mobile fall back to a clean, legible vertical document of the same clusters.
- No em dashes in any rendered copy or code comments. Design tokens defined centrally and reused.

## Deliverables

- The graph page + cluster components + the spine/playhead + tokens, wired into the home route so it renders.
- The vertical fallback working under reduced motion and on mobile.
- Brief note in the PR/summary of any decisions made on the still-open items (snap physics, render tech, typeface, the named-investor list). If you change a design decision, update the relevant spec in `boardy-pro-research/` in the same change.
- A screenshot or short clip of the result if the environment can produce one.
