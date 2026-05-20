# Bhutan Blockchain Training 2026 — Hackathon Winners

A full-screen winner-reveal presentation. Six slides that build suspense:
title → community favourite → runner-up build-up → runner-up reveal →
champion build-up → champion reveal. Silver confetti for runners-up,
gold-with-prayer-flag-colours confetti for the champion.

**Live deck:** https://bhutan-hackathon-winners.vercel.app

It is one self-contained `index.html` file — no framework, no build
step. All CSS and JS are inline. The slide controller is ~30 lines of
vanilla JS at the bottom of the file.

- **2nd place:** Toff — $1,300 + Devcon 2026 ticket
- **1st place:** BondChain — $1,700 + Devcon 2026 ticket

---

## Presenting it

Open the live link, or run it locally:

```bash
npx serve .
```

Controls while presenting:

- `Space` / `→` / `Enter` / `PgDn` — next
- `←` / `PgUp` — back
- `Home` / `End` — first / last
- Click the right side of the screen → next; click the left → back
- Swipe on mobile

The confetti burst fires automatically when a reveal slide becomes
active (it reads `data-confetti="silver"` or `"gold"` on the slide).

---

## Reusing it next year — the easy way

You do **not** need to know HTML. The fastest way to produce next
year's winner reveal is to let
[Claude Code](https://www.anthropic.com/claude-code) do it, guided by
the playbook prompt below.

**Steps:**

1. Install Claude Code (one-time): https://www.anthropic.com/claude-code
2. Open a terminal in an empty folder and run `claude`.
3. Copy the **entire** prompt in the grey box below.
4. Paste it into Claude Code and press enter.
5. Answer its questions one at a time — it will ask you for the event
   name, the organising bodies, the champion + runner-up + community
   favourite (team names, prize amounts, what tickets).
6. When it finishes it will publish the new deck and give you the live
   link.

Claude Code reads this repository first, so it already understands how
the reveal sequence works. You only provide the new winners.

### The playbook prompt — copy everything between the lines

> ⚠️ **If you forked this into your own GitHub account/org, replace the
> repository URL on the first line of the prompt below with your fork's
> URL** — otherwise Claude Code edits a copy you can't publish to.

```text
You are updating a winner-reveal presentation for a government
hackathon. The deck lives in this GitHub repository:

  https://github.com/technophile-04/bhutan-hackathon-winners

TASK
Clone that repository (git clone the URL into the current folder, then
cd into it). Read these files completely before doing anything else:
  - index.html  (the entire deck — one file: HTML + CSS + vanilla JS)
  - README.md   (this playbook and the conventions section at the bottom)

Then help me produce an updated reveal deck for a NEW hackathon by
interviewing me and editing index.html. Do not summarise or rewrite my
content. Keep the visual design exactly as it is — you are swapping
content, not redesigning.

HOW TO INTERVIEW ME
Ask about ONE topic at a time, show me what you are going to change,
and wait for my answer before moving on. If I say "no change" or
"keep it", leave that part exactly as it is. Go through these topics
in order:

  1. Event identity — event name (e.g. "Blockchain Skills Bootcamp &
     Hackathon · 2026"), city/month, and the closing sub line on the
     title slide ("Thimphu, May 2026. Five tracks, real citizen
     problems, two projects standing at the top.").

  2. Organising bodies — the credits row on the title slide. Currently
     three: BLOC × Ethereum Foundation × Royal Government of Bhutan.

  3. Community favourite / popularity winner — name, the TakinCoin
     amount, the truncated wallet (e.g. "5,555 TKC · 0x452c…e228"),
     and the prize line (Devcon ticket etc.). Ask whether to keep
     this slide at all — some years there is no popularity prize.

  4. Runner-up (2nd place) — team name and prize lines. Currently:
     team "Toff", "$1,300 cash prize" + "Sponsored Devcon 2026 ticket".

  5. Champion (1st place) — team name and prize lines. Currently:
     team "BondChain", "$1,700 cash prize" + "Sponsored Devcon 2026
     ticket". Plus the closing line under the card ("Built in
     Thimphu. Headed to Devcon.").

RULES YOU MUST FOLLOW (this deck has hard constraints)

  - The reveal sequence is the whole point. Each prize has TWO slides:
    a build-up slide ("first, our 2nd…" / "and now, our 1st…") and
    then the reveal card. Runner-up is revealed BEFORE the champion.
    Do not collapse the build-up slides into the reveals; the pacing
    is what makes it feel like a reveal.

  - Confetti palette is set per slide by data-confetti="silver" or
    data-confetti="gold". Silver for runners-up and the popularity
    prize; gold (which includes the Bhutanese prayer-flag colours) is
    reserved for the champion. Match the existing pattern when adding
    or reorganising slides.

  - Single HTML file, vanilla JS, no framework. Do not introduce a
    build step, a bundler, React, or any dependency. All CSS and JS
    stay inline at the top and bottom of index.html.

  - Preserve the visual identity. The night-sky gradient, the rotating
    dharma-sun halo, the mountain SVG silhouette at the bottom, the
    prayer-flag strip at the top, the Fraunces display + Spline Sans
    body fonts, and the gold accent palette together are the deck's
    look. Do not change them unless I explicitly ask.

  - Title Case stays Title Case. Unlike a different deck I have, this
    one is intentionally in normal sentence / Title Case. Do not
    lowercase team names, prize lines, or headings.

  - Do not open the deck in a browser or take screenshots to "check"
    it. Reason from the HTML/CSS/JS directly. Everything you need
    (sizes, colours, animation timings) is in the source.

WHEN DONE
  - Sanity check: the number of `<section class="slide` openings
    matches what you expect (one per slide), and each reveal section
    still has its data-confetti attribute.
  - Run: git add -A && git commit && git push
  - The repository is connected to Vercel, so pushing automatically
    publishes the new deck. Tell me the live URL and a short summary
    of what changed. If the push fails because this is a fresh fork
    with no Vercel link yet, tell me and walk me through running
    `npx vercel` then `npx vercel git connect`.
```

---

## Reusing it manually (if you'd rather edit it yourself)

Everything is in `index.html`. Each slide is one
`<section class="slide">`. Reveal slides carry
`data-confetti="silver"` or `data-confetti="gold"` — the JS at the
bottom of the file watches for the active slide and fires the matching
confetti burst.

To add a slide, copy an existing `<section class="slide">`, paste it
where you want it in the reveal order, and update its content. The
navigation dots and confetti both adapt automatically based on the
sections found in the DOM.

Push to the `master` branch and Vercel redeploys automatically. If you
forked this into a brand-new repository, link it once with
`npx vercel` and `npx vercel git connect`.

---

## Conventions cheat-sheet

These are the rules baked into the deck. The playbook prompt repeats
them so Claude Code follows them, but they are here for humans too.

| Area | Rule |
|---|---|
| **Reveal pattern** | Each place gets a build-up slide *and* a reveal card. Runner-up revealed before champion. |
| **Confetti** | `data-confetti="silver"` for runners-up / popularity; `data-confetti="gold"` for the champion (gold palette mixes in prayer-flag colours). |
| **No framework** | Single HTML file, inline CSS + vanilla JS. No bundler, no React, no dependencies. |
| **Visual identity** | Night-sky gradient, dharma-sun halo, mountain silhouette, prayer-flag strip, Fraunces + Spline Sans, gold accents. Preserve. |
| **Casing** | Title / sentence case throughout. Do NOT lowercase content (unlike the briefing deck, which is intentionally lowercase). |
| **Deploy** | Push to `master` → Vercel auto-publishes. Fresh fork → `npx vercel` + `npx vercel git connect` once. |

---

> ⚠️ **Forked this?** Before using the playbook prompt, replace the
> repository URL on its first line with your own fork's URL —
> otherwise Claude Code edits a copy you can't publish to.

BLOC × Ethereum Foundation × Royal Government of Bhutan
