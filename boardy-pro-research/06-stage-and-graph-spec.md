# Boardy Pro: Stage & Graph System Spec (decisions locked)

Status: final system spec for the living network. This supersedes the old centered-monument hero. There is no hero section anymore. The whole page is one node-edge graph you scroll left to right. Decisions made in brainstorm:

- **Architecture:** the entire page is a single connected node-edge graph. Horizontal scroll, left to right. Non-negotiable.
- **Direction means something:** rightward is connector to closer, intro to closed deal. Guided linear path with gentle magnetic snaps onto each stop.
- **Boardy:** a quiet left anchor whose brass edges fan rightward across every screen. He bookends (present at the entry, returns at the close). Not a centered monument, not a re-introduction.
- **Wayfinding:** a bottom deal-track spine with a playhead. Stops: Intro, Proof, Pipeline, Differentiator, $8M round, Network, Close. No minimap.
- **Your graph:** the visitor's own network. A dim "You" node that comes alive across the journey and ends clickable. Real logos/investors in the outer ring, archetypal role-labels near you.
- **Motion:** subtle life. Edges draw on arrival, your node comes alive, the playhead is the line between done and possible, the differentiator is a dying edge. Respect `prefers-reduced-motion`.
- **Conversion:** phone-first. Live phone field at the Close, persistent "Talk to Boardy" docked on the spine.
- **No eyebrow line.** The locked headline carries the framing at the entry.

The cluster-by-cluster content lives in [07-cluster-flow.md](07-cluster-flow.md). This file is the system: the stage, the graph language, the spine, the scroll, motion, and accessibility.

---

## 1. Concept

The page is a living network. Boardy is the superconnector, so the page behaves like a network you travel through. You enter at the far left where Boardy sits as a quiet brass anchor, his edges already fanning rightward. As you scroll right, you watch your own graph come alive: Boardy wires you into proof, then a pipeline, then the room full of investors and notable people, then he closes the deal and your node lights up. Rightward is the whole thesis encoded as motion: connector becomes closer, intro becomes closed deal.

Reject the generic dark-mode-glow hero. The product is a network, so the page is a network.

**Attention order at the entry:** locked headline -> the dim "You" node -> Boardy's fanning brass edges -> the deal-track spine.

---

## 2. Color palette (carried forward, extended for the graph)

### Background (cool dark stage)
| Token | Hex | Use |
|---|---|---|
| `bg-base` | `#0B0E14` | The stage, cool charcoal-black, the void the graph floats in |
| `bg-radial-lift` | `#141A26` | Faint radial lift behind the active cluster, travels with the playhead |

Keep it cool. Warm bg kills the brass.

### Brass (character + edges + nodes + spine, the graph material)
| Token | Hex | Use |
|---|---|---|
| `brass-highlight` | `#E8C98A` | Specular highlights, node rims, spine keyline, hot edge of a freshly drawn connection |
| `brass-mid` | `#C99A4B` | Core brass tone, made edges, node fills |
| `brass-shadow` | `#8A6A2E` | Recesses, node undersides, edge falloff |

### Edge & node states (the grammar of the graph)
| Token | Value | Use |
|---|---|---|
| `edge-made` | `brass-mid` -> `brass-highlight`, full opacity | Edges behind the playhead. A connection that happened. |
| `edge-potential` | `brass-mid` at ~22% opacity, dashed | Edges ahead of the playhead. A connection that could happen. |
| `edge-drawing` | `brass-highlight` head with a brass trail | The animated state as an edge is drawn on arrival |
| `edge-dying` | `brass-mid` desaturating to `#3A3F49`, dashing wider | The stalled follow-up edge in the Differentiator |
| `node-real` | brass rim, dark fill, logo/name inside | a16z, Sequoia, Anthropic, named investors/operators |
| `node-archetype` | brass rim, dimmer, role-label inside | "a Series A lead, one intro away" |
| `node-you-dim` | `#5A6273` rim, no fill glow | The "You" node before it is connected |
| `node-you-live` | `boardy-blue` rim + soft blue glow | The "You" node once it is fully connected, clickable |

### Spotlight / light (warm white, used sparingly)
| Token | Hex | Use |
|---|---|---|
| `spot-core` | `#FCF6EA` | Warm-white light behind Boardy at the entry and at the close |
| `spot-mid` | `#EBD9B4` | Soft gold-tinted falloff |
| `spot-edge` | transparent | Fades to nothing |

Warm-white, never peach, never saturated. It marks where Boardy stands (entry and close), not every cluster.

### Boardy blue (the interactive color)
| Token | Hex | Use |
|---|---|---|
| `boardy-blue` | `#2D7DD2` | The live "You" node, phone-field submit, links, focus ring |
| `boardy-blue-hover` | `#246BB8` | Hover |

Rule: **brass = Boardy, edges, nodes, spine. blue = the live "You" node and anything clickable.** No third brand color.

### Text + accent
| Token | Hex | Use |
|---|---|---|
| `text-primary` | `#F5F3EE` | Headlines, cluster labels, warm off-white |
| `text-secondary` | `#A8B0BD` | Body, node sublabels, cool muted grey |
| `text-offer` | `#E8C98A` | "Free for your first year" (brass) |
| `field-bg` | `#161B24` | Phone field fill |
| `field-border` | `#2A3340` | Phone field border (focus -> boardy-blue) |
| `accent-red` | `#B23A2E` | Tie-red. Tiny accents only |

---

## 3. Typography

Display grotesk, heavy. Recommended **Space Grotesk** or **Archivo** (free, bold, characterful). Body in the same family or Inter.

| Element | Size (desktop) | Weight | Color | Notes |
|---|---|---|---|---|
| Entry headline | 64-80px (clamp) | 700 | `text-primary` | Two lines, leading ~1.05, lands at t=0 |
| Cluster label | 28-40px | 700 | `text-primary` | The named-destination title on arrival |
| Cluster body | 20-22px | 400 | `text-secondary` | Max ~520px |
| Stat / big number | 56-96px | 800 | brass gradient | Proof and $8M callouts |
| Node label (real) | 15-17px | 600 | `text-primary` | Logo or name |
| Node label (archetype) | 14-15px | 500 | `text-secondary` | "a 3-time founder" |
| Spine stop label | 13-14px | 600 | `text-secondary` (active -> brass) | The deal-track stops |
| Field input text | 18px | 500 | `text-primary` | |
| Submit button | 17-18px | 600 | white on blue | |
| Offer microcopy | 14-15px | 500 | `text-offer` | |

Mobile: the entry headline clamps ~36-40px; cluster labels ~24-28px.

---

## 4. The graph language (how nodes and edges read)

The whole page is built from three primitives. Get these consistent and the page feels like one world.

### Boardy (the anchor)
- The brushed-brass character (`golden boardy pro.png`), seated at the far left, in a warm-white pool of light.
- From him, **brass edges fan rightward**, splaying across the screen toward every node you meet. The fan is always visible, even when Boardy himself has scrolled off the left edge, so every connection visibly originates from him.
- He returns at the Close, on the right, to receive your now-lit node.

### Nodes
- A node is a brass-rimmed disc on the dark stage. Inside it is either a real logo/name (`node-real`), an archetypal role-label (`node-archetype`), a stat, or the visitor (`node-you`).
- The **"You" node** is the throughline. It starts at the center-edge as `node-you-dim`, grey and unlit. Each cluster it gains one more connection and a little more light. By the Close it is `node-you-live`: brass-connected, Boardy-blue rimmed, glowing, and clickable.

### Edges
- Edges are the brass lines between nodes. Their **state encodes time**:
  - **Behind the playhead -> `edge-made`** (solid brass). A connection that happened.
  - **Ahead of the playhead -> `edge-potential`** (dim, dashed). A connection that could happen.
  - The playhead is the moving boundary between the two. Scrolling right is the act of converting potential edges into made edges. This is the connector-to-closer thesis, drawn.
- **Edges draw on arrival.** When the playhead settles on a cluster, the edges into that cluster's nodes animate from Boardy outward (`edge-drawing`: a bright brass head pulling a trail), then settle to `edge-made`. You watch Boardy wire you in, live. The drawing is the product working, never idle decoration.

---

## 5. The deal-track spine (wayfinding)

A thin horizontal spine pinned to the bottom of the viewport, present on every cluster.

- **Stops, left to right:** `Intro -> Proof -> Pipeline -> Differentiator -> $8M round -> Network -> Close`.
- **Playhead:** a brass marker that slides right as you scroll, sitting on or between stops. It answers the two questions a minimap cannot: how far am I, and what is coming.
- **Behind/ahead styling:** stops behind the playhead read brass (done); the stop under the playhead is highlighted; stops ahead are muted (`text-secondary`). The spine itself mirrors the edge grammar: brass to the left of the playhead, dim to the right.
- **Draggable scrubber:** the playhead is draggable. Grab it and scrub the whole journey. It is a control, not just a readout.
- **Named-destination labels:** on arrival at a cluster, its label animates in (e.g. "Pipeline"), so you always know where you landed.
- **Docked CTA:** a small persistent "Talk to Boardy" sits at the right end of the spine (or a pinned corner), so conversion is always one tap away no matter where you strand. It is the only blue element that travels with you.
- **No minimap.** Horizontal motion is the map; the spine is the legend.

---

## 6. The horizontal scroll (get this right or the concept fails)

The scroll is the single biggest risk. It must feel as good as native vertical scroll or the whole idea reads as a gimmick.

- **Input mapping:** vertical wheel / trackpad / touch maps to horizontal travel through the graph. Touch swipe is horizontal. Keep the mapping close to 1:1 and natural; no acceleration tricks that fight the user.
- **Magnetic snap:** gentle snaps settle the viewport onto each cluster so you never strand in the void between clusters. The snap is soft (ease, not yank) and only engages near a cluster, so free scrubbing between stops still feels smooth.
- **Keyboard:** `ArrowRight` / `ArrowLeft`, `PageDown` / `PageUp`, and `Space` advance and retreat by cluster. `Home` / `End` jump to Intro / Close. Tab order follows the clusters left to right.
- **Deep links:** every cluster has a hash route (`/#intro`, `/#proof`, `/#pipeline`, `/#differentiator`, `/#round`, `/#network`, `/#close`). The back button moves between visited clusters. Landing on a deep link starts at that cluster with the graph already drawn up to there.
- **First paint:** before any scroll, the entry frame shows the locked headline (carrying the full meaning), Boardy as the anchor, the dim "You" node, and the spine. Value lands at t=0. The graph is texture behind the sentence; the sentence is the message.
- **Reduced motion / mobile fallback:** see section 8. Under reduced motion the horizontal hijack is disabled entirely and the page is a normal vertical document.

---

## 7. Motion spec (subtle life only)

Quiet and premium. Respect `prefers-reduced-motion` (disable all of the below if set, and fall back to the vertical document).

- **Edges draw on arrival** (principle 1): on settling at a cluster, edges animate from Boardy to that cluster's nodes over ~500-700ms ease-out, bright brass head pulling a trail, then settle to `edge-made`.
- **Your node comes alive** (principle 2): at each cluster the "You" node gains one connection and steps up in brightness. The step is small per cluster; the cumulative effect across the scroll is the payoff. At the Close it crosses fully to `node-you-live` (blue, glowing).
- **Playhead is the line between done and possible** (principle 3): as the playhead passes an edge, that edge transitions `edge-potential -> edge-made` (dashed/dim to solid/bright) in sync with the scroll. Scrubbing backward reverses it.
- **The differentiator is a dying edge** (principle 4): in the Differentiator cluster, a single edge flatlines (its brass desaturates, the dash widens, it sags and fades to `edge-dying`), then Boardy sends a pulse down it and it snaps back to `edge-made`. The literal image of "the follow-up is where deals die, and where I win."
- **The $8M self-loop:** Boardy's edge curves out and loops back into himself; the loop draws once on arrival and then holds with a slow brass shimmer. The playhead parks. This is the peak; let it breathe.
- **Brass shimmer:** a slow, low-opacity specular sweep across made edges and node rims on a long loop (~6-8s), barely there. Sells the metal.
- **Field focus:** the phone-field border transitions to `boardy-blue` with a soft glow.
- **No:** parallax jank, bouncing, looping character animation, anything that pulls focus from the headline, the active cluster, or the field. If a flourish competes with the message, cut it.

---

## 8. Accessibility & the vertical fallback

The vertical version is not an afterthought. It is the legible source of truth and the accessible path. Build it first.

- **`prefers-reduced-motion: reduce` and small viewports** collapse the graph to a clean **vertical** stack of the same clusters, scrolled normally top to bottom. Same content, same copy, same order (Intro -> ... -> Close). Edges become simple static connectors or are dropped; nodes become labeled cards; the spine becomes a standard progress indicator or is dropped.
- Each cluster is a semantic landmark (`<section>` with a heading). The entry headline is the single `<h1>`.
- The graph canvas has a text alternative; node logos/names have real `alt` / labels. Screen readers get the cluster copy in order, never a soup of floating nodes.
- The phone input has a real (visually-hidden if needed) `<label>`, `type="tel"`, `inputmode="tel"`, `autocomplete="tel"`. Visible focus on input and button (the blue ring counts).
- Keyboard reaches every cluster and the CTA without a mouse (see section 6).
- Text contrast passes WCAG AA against the dark stage (the chosen tokens do; keep it that way).

---

## 9. Boardy at the bookends

- **Entry (far left):** the brushed-brass character in a warm-white pool, edges already fanning rightward. He is the origin of the graph. He is smaller and calmer than the old monument; he anchors, he does not pose.
- **Close (far right):** Boardy returns to receive your now-lit node. The warm-white light returns (palette callback), the self-loop and the lit "You" node share the frame, and the phone field sits with him. The page bookends: it opens and closes on Boardy and light, with the whole network strung between.
- Do not recolor or regenerate the character. Brushed brass box, blue face intact, navy suit, white shirt, red tie.

---

## 10. Assets

- Character: `golden boardy pro.png` (brushed brass box, blue face, navy suit, red tie, chest-cropped, transparent bg). Lives in the parent project folder; move into the app's public dir on build.
- Graph (nodes, edges, fanning brass, spine, playhead, self-loop): build as SVG or canvas with live gradients, not raster. Live text for headlines and labels.
- Real logos for the outer ring: source clean monochrome/brass-tintable marks. Confirm the named list and framing before printing (see Don'ts).
- Fonts: Space Grotesk / Archivo (self-host or Google Fonts).

---

## 11. Don'ts

- No warm/orange background. Cool dark only, or the brass dies.
- No third brand color. Brass + blue + (tiny) red is the whole system. Blue is reserved for the live "You" node and clickable things.
- No em dashes.
- Don't let the scroll fight the user. If the horizontal scrub does not feel as good as native vertical, fix it or escalate; do not ship a gimmick.
- Don't strand the visitor between clusters (magnetic snap) or hide the exit (docked CTA).
- Don't imply endorsement. Real logos and named investors are "the rooms I can get you into", not "these people vouch for you". Inner role-labels stay archetypal, never named real people. Verify the list before printing.
- Don't make the first paint a puzzle. The headline carries the meaning before anyone scrolls.
- Don't over-animate. Motion is the product working (edges drawing, node lighting), not flourish. If it competes with the message, cut it.
- Don't add an email/password signup. Phone-first only.
- Don't treat the vertical fallback as second-class. It is the accessible, legible source of truth.
