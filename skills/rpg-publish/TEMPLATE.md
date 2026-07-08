# {Adventure Title}

<!--
  Published structure. Audience wall follows ADR 0002:
    - Default is GM. A section is player-facing ONLY if tagged {.player}.
    - Promote:  ## Player Pitch {.player}   (cascades to nested headings
                until the next same-or-higher heading)
    - Demote a secret back to GM inside a player section:
        block:  ::: gm  … :::        inline:  [text]{.gm}
    - Fail-safe: an untagged secret stays hidden. When unsure, leave it GM.
  Cross-links: linkify STRUCTURED references only — (Scene 8), an NPC block,
    GM Notes: X, a named clock — never bare names in prose. Use markdown
    anchors, e.g. [Scene 8](#8-grandfathers-hand), [Roke](#colonel-ambrose-roke).
  Print: put \newpage before each major section for clean pagination.
-->

## Description {.player}

*One or two sentences — the broadest outline, spoiler-free.*

**System** · one-shot / campaign · **~N hours** · **N players**

## Player Pitch {.player}

Two or three persuasive paragraphs: why this session is fun, what it contains,
the flavour and the promise. Player-facing — twists stay out, or are alluded to
at most ("…but of course it's not that simple"). This is a *sell*. Be exciting.

\newpage
## GM Pitch

The full story in a few tight paragraphs: the real situation, the major beats in
order, the surprises and reveals, and how it ends. Everything the Player Pitch
withholds. A GM reads this once and knows the whole shape of the night.

## GM Summary

One page the GM can run from at a glance. Keep it dense and scannable.

- **Clocks:** each named clock, its size, what fills it, what it triggers.
- **NPCs:** one line each — who they are and the single lever they offer. Link to
  the full block: [Name](#anchor).
- **Scenes:** the sequence/map — fixed beats vs. floating scenes, the master clock.
- **Remember:** the 3–6 easy-to-drop facts that break the session if forgotten.

\newpage
## NPCs

### {Major NPC Name} — "{epithet}"
- **Look:** Physical description — the fixed sensory signature the GM plays every time.
- **Wants:** The driving goal.
- **Secret:** What players can uncover. [Demote a hard spoiler with ::: gm if this
  block is ever promoted.]
- **Voice:** Non-scene dialog — one or two lines to improvise their manner from,
  distinct from scripted scene lines.

<!-- Lead with the essential majors. Then minors, compressed: -->

### Minor NPCs
- **{Name}** — role in one clause; the one lever or fact they carry; a voice line if it earns its place.

\newpage
## Scenes

### {N}. {Scene Name} *(fixed / floats)*
- **Setting:** Where, who's present, the read-aloud sensory hit.
- **Core dialog:** The one or two lines worth scripting.
- **Clocks / combat:** Which clock ticks here; any encounter and its stakes.
- **Outcome → adventure:** How the ways this resolves change what comes next — the
  consequence that carries forward. *(This is the load-bearing line; keep it concrete.)*

<!-- Repeat per scene, in play order. Sequence loosely; mark floating scenes. -->

\newpage
## Pregens {.player}

*Optional. Player-facing sheet, then what the GM knows, walled per pregen.*

### {Character Name} — "{handle}"
- **Look / Bio / Vice:** Player-facing character info.
- **Hook:** Their personal thread into tonight (player-safe framing).

::: gm
**GM knows:** the character's secret, their tie to an NPC, the reveal they trigger.
:::

\newpage
## Handouts

*Optional. In-fiction artifacts handed to players — letters, briefings, dossiers.*
*Each is player-facing content; render separately as a Handout artifact.*

\newpage
## GM Notes & Lore

Everything load-bearing that doesn't fit above: the full truth behind the premise,
how to run the hard beats, rules rulings, the release/rite mechanics, safety dials.
Terse and organized under sub-headings; a reference, not an essay.
