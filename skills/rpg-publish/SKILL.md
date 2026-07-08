---
name: rpg-publish
description: Condense a finished, critique-revised adventure into a tight, dual-audience, publish-ready Markdown document — Description, Player Pitch, GM Pitch, GM Summary, NPCs, Scenes, optional Pregens and Handouts, GM Notes — with the GM/Player audience wall (ADR 0002 tags) and hyperlinked cross-references, then offer to render it to a print PDF and a hyperlinked wiki. Use when the author wants to finalize, publish, condense, tighten, or make an adventure shareable/table-ready; NOT for authoring (rpg-dev), critique (rpg-critic), or applying a critique (rpg-revise).
---

# RPG Publish — Condense an Adventure for Sharing

Turn a discursive adventure — one that's been through [rpg-dev](../rpg-dev/SKILL.md)
and the [rpg-critic](../rpg-critic/SKILL.md)/[rpg-revise](../rpg-revise/SKILL.md) loop —
into a **tight, playable, shareable document**: no extraneous prose, a clean GM/Player
wall, and hyperlinked cross-references, ready for print and as an electronic reference.

You are **compressing and reorganizing, not rewriting**. The critique loop already
decided what the adventure *says*; publish decides how little it can take to say it.
Golden rule: **a GM must be able to run the whole session from the published doc alone.**

## Workflow — one pass, then review

1. **Read everything first.** The source adventure, and its `*-critique*.md` if present
   (so you honour choices the author already made). Confirm the source path, then write to
   `<adventure-slug>-published.md` **beside the source** — never touch the source file.
2. **Draft the whole document in one pass** into the canonical structure
   ([TEMPLATE.md](TEMPLATE.md)): Description, Player Pitch, GM Pitch, GM Summary, NPCs,
   Scenes, optional Pregens, optional Handouts, GM Notes & Lore. Condense, tag audience,
   cross-link (below) as you go.
3. **Report the cuts.** After writing, give a short list of what you compressed, merged,
   or dropped — especially judgment calls — so the author can restore anything load-bearing.
   Don't bury a real cut; list it.
4. **Offer to render.** The render scripts ship with this skill under `scripts/` (resolve
   relative to this SKILL.md): `scripts/pdf.sh <file>` for the print packet;
   `scripts/gen-cards.py` for pregen selection cards; `scripts/render-cards.sh` to turn a
   card HTML into a one-page PDF; the wiki HTML for the hyperlinked reference. Offer, don't
   assume. (`pdf.sh` needs `pandoc` + `xelatex`; `render-cards.sh` needs headless Chrome.)

## What to cut, what to keep

**Cut** — the discursive residue, aggressively:
- The same fact restated across Premise, an NPC block, and GM Notes → state it **once**, in
  its right home, and link to it.
- Prep meta-commentary and reassurance ("toolbox roster, not a checklist", "play it as
  tragedy not a gotcha") → compress to a one-line GM steer, or drop.
- Hedging, parenthetical asides that duplicate the main text, authoring scaffolding
  (name etymologies, resolved Open Threads).

**Keep** — everything table-relevant, losslessly:
- Every NPC's Look / Wants / Secret / Voice, and every scripted or improv dialog line.
- Every clock (size, fill, trigger), number, stat block, scene branch, and — critically —
  **each scene's outcome→consequence**: how the way a scene resolves changes what follows.
- The reveal order and what the crew know vs. discover.

If something load-bearing is *missing* from the source (an absent clock value, a stat block),
**flag it in the cut report — never invent it.** Preserve the module's terse, table-ready voice.

## The audience wall (ADR 0002 — fail-safe)

Content is **GM by default**. Promote only the genuinely player-facing:
- **Player-facing:** Description, Player Pitch, and each Pregen's player card fields →
  tag the heading `{.player}` (cascades to nested headings until the next same-or-higher one).
- **Demote a spoiler** sitting inside a player section back to GM: `::: gm … :::` (block) or
  `[…]{.gm}` (inline).
- **When unsure whether something is a spoiler, leave it GM.** A secret reaches players only by
  deliberate promotion; a forgotten tag hides, never leaks. The Player Pitch must not give away
  a twist.

## Cross-linking (structured references only)

Linkify **structured** references — `(Scene 8)`, an NPC named in a scene, `GM Notes: X`, a named
clock — with markdown anchors: `[Scene 8](#8-grandfathers-hand)`, `[Roke](#colonel-ambrose-roke)`.
**Never auto-link bare names in prose.** Put `\newpage` before each major section so the print PDF
paginates cleanly.

## Stance

- Publish reorganizes and compresses **existing** content — it never adds material or re-critiques.
  If you spot a genuine contradiction while condensing, note it in the cut report; don't silently fix
  it (that's [rpg-critic](../rpg-critic/SKILL.md)/[rpg-revise](../rpg-revise/SKILL.md)).
- One adventure = one `-published.md`; regenerable, so a re-run nukes and replaces it. The source and
  critique files stay untouched.
- Terse over complete-sounding. If a sentence doesn't change what happens at the table, cut it.
