---
name: rpg-dev
description: Collaboratively develop tabletop RPG adventures — premise, NPCs, and scenes — and capture them as a durable Markdown file. Use when the user wants to design an adventure, module, one-shot, or session; develop a premise, scene, or NPC; or mentions running/prepping a game.
---

# RPG Dev — Adventure Creation

Build an adventure *with* the user, one layer at a time, and persist it to a single
Markdown file. Never dump a finished adventure from one prompt — interview, propose,
and confirm at each layer.

## Workflow

Work top-down. Do not advance a layer until the user is satisfied with the current one.

1. **Premise** — establish the spine before anything else:
   - The situation (what is happening, and why now)
   - The stakes (what goes wrong if no one intervenes)
   - The hook (why *these* characters get pulled in)
   - Tone & scale (gritty vs. heroic; one-shot vs. multi-session)
   Propose 2–3 premise options as short pitches; let the user pick or remix.

2. **Scenes** — the units of play. For each, develop:
   - Purpose (what this scene is *for* in the arc)
   - Setting and who's present
   - What's at stake / what can change here
   - Ways in and ways out (how players arrive, how it resolves or escalates)
   - Complications the GM can drop in
   - Sensory details: What does this place look like, sound like, smell like
   Sequence scenes loosely — offer branches, not a railroad.

3. **NPCs** — the people who drive the situation. For each, develop:
   - Role in the premise, and what they **want**
   - A **secret** or complication the players can uncover
   - Voice/manner (one line the GM can improvise from)
   - Visual description. Hair cut, face, build, style and key items of dress.
   - Be creative with names no Elara, Kael, Thorne, Voss, no -ae-, no noun-surnames. Name the linguistic origin of each name proposed.
   Start with the 2–4 NPCs the premise can't exist without; add minor ones later.

4. **Persist** — write everything to the adventure file after each layer, not just at
   the end. See [TEMPLATE.md](TEMPLATE.md) for the file structure.

## Artifact rules

- **One adventure = one file.** Default path: `<campaign-slug>\<adventure-slug>.md` in the working
  directory. Confirm the filename with the user on first write.
- Sections follow [TEMPLATE.md](TEMPLATE.md): Premise, NPCs, Scenes, plus optional
  GM Notes and Open Threads.
- Artifacts are **standalone** — no cross-links between files.
- Update the file incrementally as each layer is confirmed; keep it the single source
  of truth so a fresh session can pick up the adventure from the file alone.

## Interaction style

- Ask focused questions; offer concrete options rather than open-ended prompts.
- Prefer the user's ideas over your own — you are a collaborator, not the author.
- Track loose ends in the **Open Threads** section so nothing gets dropped between
  sessions.
- Be efficient and direct with scene description and NPC dialog. Write direct examples to the document.
