# Design Prompt: Boardy Pro Living Network (for claude.ai/design)

Paste the prompt below into claude.ai/design. **Attach `golden boardy pro.png`** (the brushed-brass Boardy) and reference it as the anchor character. This generates the visual language for the page (the stage, the graph, a key frame or two), not a generic hero. The canonical source of truth is [`boardy-pro-research/06-stage-and-graph-spec.md`](../boardy-pro-research/06-stage-and-graph-spec.md) and [`07-cluster-flow.md`](../boardy-pro-research/07-cluster-flow.md). If anything here conflicts, the specs win.

---

Design the visual language for a landing page for **Boardy Pro**, the premium tier of Boardy, an AI "superconnector" that calls you, learns what you are building, and makes warm introductions. Pro is the upgrade where Boardy stops at introductions and starts closing deals. The brand voice is "half OpenAI, half Pixar": frontier tech with a warm, playful character.

**The core idea: the whole page is a living network you travel through.** Not a hero with sections under it. One connected node-edge graph, scrolled horizontally left to right. The direction means something: rightward is connector to closer, from the intro to the closed deal. You watch your own network come alive as Boardy wires you into investors and notable people, then closes the deal.

**The character (attached image, use it as the anchor, not a centerpiece monument):** Boardy is a figure with a brushed-brass cardboard-box head, a friendly blue smiley face and two blue dot eyes, wearing a navy suit, white shirt, and red tie. The brass box is the premium signal. Do not recolor him. He sits as a quiet anchor at the far left of the graph, in a warm-white pool of light, and his brushed-brass edges fan rightward across the screen toward everything you meet, so every connection visibly originates from him. He bookends the page: present at the far-left entry, returning at the far-right close.

**The stage:** a cool, near-black background (deep charcoal with a slight blue-slate undertone, around #0B0E14). The graph (nodes and brass edges) floats on this void. Keep the background cool. Warmth anywhere would mute the brass and ruin the effect. Warm-white light appears only where Boardy stands (entry and close), never peach, never saturated.

**The graph language (the heart of the design):**
- **Nodes** are brass-rimmed discs on the dark stage. Inside: a real company logo or investor name (the outer ring, the aspiration), a flattering archetypal role-label like "a Series A lead, one intro away" (near the visitor, the personal pull), a stat, or the visitor themselves.
- **The "You" node** is the throughline: a single node that starts dim and grey at the center-edge, unlit and unconnected, then gains a connection and a little more light at every stop, and ends fully lit in Boardy-blue, glowing and clickable.
- **Edges** are brass lines whose state encodes time: solid bright brass behind the playhead (a connection that happened), dim and dashed ahead of the playhead (a connection that could happen). Edges animate being drawn from Boardy outward as you arrive at each cluster. You watch him wire you in.

**Wayfinding: a deal-track spine.** A thin horizontal spine pinned to the bottom with a sliding playhead. Stops left to right: Intro, Proof, Pipeline, Differentiator, $8M round, Network, Close. Stops behind the playhead read brass (done); ahead read muted. A small persistent "Talk to Boardy" stays docked at one end.

**The peak frame to render: the $8M self-loop.** At the "$8M round" stop, Boardy's brass edge curves out and loops back into himself instead of pointing at another node. The proof he closed his own funding round on his own platform. The plain claim "I raised my own funding round. On myself." sits on the loop. This is the most important single frame; render it.

**Palette (use exactly):**
- Stage background: #0B0E14 (cool near-black)
- Warm-white light at the bookends: #FCF6EA fading through soft gold #EBD9B4 to transparent
- Brass (character, edges, nodes, spine): highlights #E8C98A, mid #C99A4B, shadows #8A6A2E
- Interactive blue (the live "You" node and the CTA only): #2D7DD2
- Primary text: warm off-white #F5F3EE
- Secondary text: muted cool grey #A8B0BD
- Tiny red accent (tie only): #B23A2E
Brass is the character, the edges, the nodes, and the spine. Blue is reserved for the live "You" node and clickable things only. No third color.

**Typography:** a heavy, modern display grotesk (Space Grotesk or Archivo feel). The entry headline is large and bold, two lines, tight leading. Cluster labels are bold and smaller. Body is lighter.

**Copy for the entry frame (use verbatim, no em dashes anywhere):**
- Headline, two lines:
  "I'm done making intros."
  "Now I make deals happen."
- Subhead: "I pressure-test the fit, sit in on the calls, and chase the follow-ups so the deal actually closes. You take the win."

**Copy for the close frame:**
- Cluster label: "One closed deal pays for a decade of me."
- A single inline phone-number field with a button: placeholder "Your phone number", button label "Talk to Boardy" (button in blue #2D7DD2).
- Under it, in small brass text: "Free for your first year."

**Conversion detail:** the call to action is a phone-number field, not a "sign up" button, because Boardy literally calls you. At the close, the visitor's now-lit blue "You" node is itself clickable and focuses the field.

**Feel and finish:** premium, cinematic, lots of dark negative space, brass catching light, the network strung across the void. Subtle sense of edges being drawn and a node coming alive. Avoid clutter, avoid stock-photo gradients, avoid anything that reads as a default template. It should feel like traveling through a network, not reading a brochure.

Make it responsive: on small screens the horizontal graph collapses to a clean vertical stack of the same clusters (Intro at top, Close at bottom), scrolled normally top to bottom. Same content, same order, legible without the animation.
