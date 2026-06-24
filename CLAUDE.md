# CLAUDE.md

Working notes for any agent (cloud or local) picking up this repo. Read this before touching anything, then read [boardy-pro-research/06-hero-spec.md](boardy-pro-research/06-hero-spec.md) and [boardy-pro-research/07-section-flow.md](boardy-pro-research/07-section-flow.md).

## What this project is

A landing page for **Boardy Pro** (the paid tier of boardy.ai, the AI superconnector). Currently in brainstorm + spec phase. The specs in `boardy-pro-research/` are the source of truth. No page has been built yet.

The core story the whole page tells: **connector becomes closer.** Free Boardy makes intros, Pro closes deals. Headline is locked: "I'm done making intros. Now I make deals happen."

## Hard rules (do not violate)

- **No em dashes.** Anywhere. Not in copy, not in docs, not in code comments. Use periods, commas, or two sentences. This is a standing user preference.
- **Voice is Boardy, first person.** Boardy speaks as "I" / "me", warm, direct, a little cheeky. Never write as a company describing a product. "I'll chase the follow-up", not "Automated follow-up management". CTAs are personified ("Talk to Boardy", not "Sign Up"). See `03-voice-and-copy.md`.
- **Palette is brass + Boardy blue + cool dark.** Brass for the character, PRO, and the arc keyline. Boardy blue (`#2D7DD2`) for anything clickable. Cool near-black (`#0B0E14`) stage. Warm-white (`#FCF6EA`) spotlight. No third brand color. Red tie is a tiny accent only.
- **Phone-first conversion.** Boardy calls you. The CTA collects a phone number and routes into the boardy.ai phone-verify flow. Do NOT add email/password signup.

## Locked design decisions (settled, do not re-litigate)

- Tech stack: **Next.js (App Router) + TypeScript + Tailwind CSS**, deploy to Vercel. Phone field captures the number and hands off to Boardy's existing onboarding/verify flow (no backend auth in this repo).
- Hero composition: **centered monument** (PRO huge + centered, brass Boardy through it, headline clean below).
- Character: **brushed brass box, blue face intact**, navy suit, red tie. Asset: `golden boardy pro.png`.
- Background: **cool near-black**, never warm or peach (warm bg mutes the brass).
- The base of the hero is **the arc**: shallow convex horizon, crisp edge, thin brass keyline, warm-white spotlight glowing behind Boardy. No brass spill into the glow yet.
- CTA: **inline phone field** in the hero, not a button-only or email form.
- Motion: **subtle life** only (entrance ease-up, slow brass shimmer, gentle glow breathe). Respect `prefers-reduced-motion`. No parallax, no bounce, no flashy loops.
- Offer: **free for your first year, then $100/mo.** Founding-member-for-life is closed; mention only as a small supporting line, never the headline.
- No eyebrow line. The headline carries the framing.

## Still open / not yet decided

- Exact arc curvature depth and keyline weight (tune by eye against the spec ranges).
- Whether to repeat the CTA as a sticky nav button or only hero + close.
- Final typeface pick (spec recommends Space Grotesk or Archivo).
- The exact endpoint/redirect the phone field hands off to (Boardy onboarding flow). Stub with a typed onSubmit for now.
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
- Build the arc and PRO as SVG/CSS (live text gradient, SVG path + radial glow), not raster.
- Start with the hero, then sections 2 (transformation) and 5 (raised its own round), the two highest-impact sections.
- Keep commits scoped and descriptive. End commit messages with the Co-Authored-By trailer.

## Repo

- Remote: https://github.com/cosmosmarkets/boardypro
- Default branch: `main`.
