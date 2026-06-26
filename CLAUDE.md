# CLAUDE.md

Working notes for any agent (cloud or local) picking up this repo. Read this before touching anything, then read [boardy-pro-research/06-stage-and-graph-spec.md](boardy-pro-research/06-stage-and-graph-spec.md) and [boardy-pro-research/07-cluster-flow.md](boardy-pro-research/07-cluster-flow.md).

## What this project is

A landing page for **Boardy Pro** (the paid tier of boardy.ai, the AI superconnector). Currently in brainstorm + spec phase. The specs in `boardy-pro-research/` are the source of truth. No page has been built yet.

The core story the whole page tells: **connector becomes closer.** Free Boardy makes intros, Pro closes deals. Headline is locked: "I'm done making intros. Now I make deals happen."

The page tells that story as **a living network you travel through.** The entire page is one connected node-edge graph. You scroll it left to right, and the direction means something: rightward is connector to closer, intro to closed deal. You watch your own graph come alive as Boardy wires you into investors and notable people, then closes the deal.

## Hard rules (do not violate)

- **No em dashes.** Anywhere. Not in copy, not in docs, not in code comments. Use periods, commas, or two sentences. This is a standing user preference.
- **Voice is Boardy, first person.** Boardy speaks as "I" / "me", warm, direct, a little cheeky. Never write as a company describing a product. "I'll chase the follow-up", not "Automated follow-up management". CTAs are personified ("Talk to Boardy", not "Sign Up"). See `03-voice-and-copy.md`.
- **Palette is brass + Boardy blue + cool dark.** Brass for the character, the edges, the nodes, and the deal-track spine. Boardy blue (`#2D7DD2`) for the "You" node and the phone CTA (anything clickable). Cool near-black (`#0B0E14`) stage. Warm-white (`#FCF6EA`) light. No third brand color. Red tie is a tiny accent only.
- **Phone-first conversion.** Boardy calls you. The CTA collects a phone number and routes into the boardy.ai phone-verify flow. Do NOT add email/password signup.

## Locked design decisions (settled, do not re-litigate)

- Tech stack: **Next.js (App Router) + TypeScript + Tailwind CSS**, deploy to Vercel. Phone field captures the number and hands off to Boardy's existing onboarding/verify flow (no backend auth in this repo).
- **The whole page is one horizontal node-edge graph**, not a stack of sections. You scroll it left to right. This is non-negotiable. (It replaces the old centered-monument hero and the old vertical section stack. Those are dead.)
- **Direction carries meaning:** moving rightward moves from connector to closer, from the intro to the closed deal. Guided linear path, not a sandbox. Gentle magnetic snaps settle you on each stop so you never strand in the void between clusters.
- **Boardy is a quiet left anchor**, not a centered monument and not a re-introduction (boardy.ai already fronts him). His brass edges fan rightward across every screen, so even when he is scrolled off-screen-left, everything you meet visibly traces back to him. He bookends: present at the start, returns at the close when your node connects. Asset: `golden boardy pro.png` (brushed brass box, blue face, navy suit, red tie).
- **The deal-track spine** is the wayfinding: a bottom spine with stops `Intro -> Proof -> Pipeline -> Differentiator -> $8M round -> Network -> Close` and a playhead that slides right as you scroll. No minimap (horizontal motion is the map). Each cluster announces itself with a named-destination label on arrival. A persistent "Talk to Boardy" stays docked on the spine so the exit is always one tap away.
- **"Your graph" is the visitor's own network.** A represented "You" node sits dim at the center-edge. Mixed population: real recognizable logos and names in the outer ring (a16z, Sequoia, Anthropic, and real investors/operators making up the bulk) for aspiration and impact; flattering, clearly-archetypal role-labels near your node ("a Series A lead, one intro away", "a 3-time founder") for the personal pull. Inner labels are archetypal, never named real people.
- **Four motion principles (locked):**
  1. **Edges draw on arrival.** As the playhead lands on a cluster, Boardy's edges animate being drawn to the new nodes. You watch him wire you in. Motion is the product working, not decoration.
  2. **Your node comes alive.** The "You" node starts dim and grey at the left, gains a connection and more light at each cluster, and ends fully lit Boardy-blue and clickable. Clicking it is the phone field.
  3. **The playhead is the line between done and possible.** Edges behind the playhead render solid brass ("made"); edges ahead render dim and dashed ("potential"). Scrolling right converts possible into done.
  4. **The differentiator is a dying edge.** "The follow-up is where deals die, and where I win" is shown literally: a stalled edge flatlines and fades, then Boardy's pulse re-activates it.
- **Peak moment: the $8M self-loop.** Boardy's edge loops back to himself, the proof he closed his own round on his own platform. The playhead parks on it. The plain claim sits on the loop so nobody misses it.
- **CTA placement:** the live phone field lives at the Close cluster (where your node connects), plus the persistent docked "Talk to Boardy" on the spine. Phone-first only.
- **Motion is subtle life**, never flashy. Respect `prefers-reduced-motion`. Under reduced motion (and on mobile), the page collapses to a clean, legible **vertical** version of the same clusters. That vertical version is the accessible fallback and the source-of-truth document. Build it first, then layer the horizontal journey on top.
- **First paint sells before interaction.** The locked headline lands at t=0 at the Intro cluster as the entry state. Value before anyone scrolls.
- Offer: **free for your first year, then $100/mo.** Founding-member-for-life is closed; mention only as a small supporting line, never the headline.
- No eyebrow line at the entry. The headline carries the framing.

## Still open / not yet decided

- Snap physics and scrub feel (magnetic snap strength, easing). Tune by hand until the horizontal scrub feels as good as native vertical scroll. If it cannot, the concept is at risk, flag it.
- Render tech for the graph (SVG vs canvas vs WebGL) and how many nodes/edges can animate before it drops frames. Performance budget is a real constraint.
- Final typeface pick (spec recommends Space Grotesk or Archivo).
- The exact endpoint/redirect the phone field hands off to (Boardy onboarding flow). Stub with a typed onSubmit for now.
- The exact list of real logos and named investors/operators for the outer ring, and the legal/credibility framing ("the rooms I can get you into", not "these people endorse you"). Verify before printing names.
- Whether the old mission beat ("AI should make us more connected, not less") survives as a single quiet grace-note near the Close, or is cut.
- The `$63B` capital-introduced stat is single-sourced; verify against the live boardy.ai counter before printing it.

## Real data (use these, rounded, do not invent)

Live boardy.ai counters as of June 2026 (JS-injected, so a static scrape shows zeros):
- ~166K people spoken with
- ~110K introductions made (exact ~114,627)
- ~$63B capital introduced (verify before use)
- 17h average time to match

Launch facts: 1M+ views and ~20K comments off 4 posts, first 5,000 Pro spots gone in 2 hours, $0 ads. Boardy reportedly raised its own $8M round (led by Creandum) on its own platform. Founder: Andrew D'Souza (ex-Clearco, $5B+ deployed).

## If you build the page

- Match the existing doc structure; keep specs and any built code in sync. If you change a decision, update the relevant spec file in the same change.
- **Build the vertical (reduced-motion / mobile) version first** as the legible source of truth, then layer the horizontal graph journey on top as the progressive enhancement.
- Build the graph (nodes, edges, the fanning brass, the spine, the playhead) as SVG or canvas, not raster. Live text for headlines and labels.
- Start with the Intro entry state and the Close cluster (the two bookends, where Boardy appears and where conversion happens), then the $8M self-loop (the peak).
- Keep commits scoped and descriptive. End commit messages with the Co-Authored-By trailer.

## Repo

- Remote: https://github.com/cosmosmarkets/boardypro
- Default branch: `main`.
