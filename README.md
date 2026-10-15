# rpg-dev-skills

A set of [Claude Code](https://claude.com/claude-code) skills for building tabletop RPG
adventures — from blank page to table-ready packet. They're system-agnostic: use them for
Blades in the Dark, Lancer, D&D, or anything else.

| Skill | What it does |
|-------|--------------|
| **rpg-dev** | Collaboratively develop an adventure — premise, NPCs, scenes — into one durable Markdown file. |
| **rpg-npc-cast** | Generate de-glamorized NPC portraits from their casting notes with Gemini 2.5 Flash Image ("Nano Banana"). |
| **rpg-critic** | Give a finished module a sharp, table-focused critical read and capture it as a critique-and-response log. |
| **rpg-revise** | Fold a human-answered critique back into the module, applying the fixes you accepted. |
| **rpg-publish** | Condense a revised adventure into a run-at-the-table document — a read-once PREP layer and a TABLE layer of pure primitives — and render it to PDF / wiki. |

The natural loop: **dev → critic → (answer the critique) → revise → publish.**

## Best Practices

Create rules, setting, and campaign lore reference docs the skills can draw on — Claude can
summarize a large rulebook into a compact representation worth keeping. You can always point
at them explicitly:

```
/rpg-dev let's create an epic fantasy tale of sacrifice and triumph over evil 
using @DnD2024.md and @ForgottenRealms.md and @SwordCoastChampions.md
```

### Let the directory structure do it instead

Better: **nest your adventures, and the skills find the context themselves.** An adventure
inherits from every directory above it, out to the repo root:

```
my-games/
  blades-68/              System — rules, setting lore
    art_style.md          the visual house look for everything in this setting
    draw-tables.md        setting-owned tables to draw scene detail from
    draw-tables-flat.md   the same tables as numbered lists, for the sampler
    the-long-con/         Campaign — campaign.md, the PCs, running clocks
      01-recall/          Adventure — the module, its critique, its published form
```

Depth is up to you — drop the campaign layer for a one-shot, add a session layer below the
adventure, name the top level whatever you like. Every skill walks the tree rather than
assuming a shape:

```
~/work/bin/python ~/.claude/skills/rpg-dev/scripts/context_stack.py path/to/adventure.md
```

Prose reference **accumulates** — read broad to narrow, and where a campaign doc disagrees
with the system book, the campaign wins. The two named assets resolve **nearest-wins**, so a
single adventure can override its system's house look. See
[CONTEXT-STACK.md](skills/rpg-dev/CONTEXT-STACK.md).

### Draw tables beat the model's defaults

A model asked to invent a detail returns the attractor — the fantasy name it has written a
thousand times, the cobbled alley, the smoky jazz club. A `draw-tables-flat.md` in your
setting directory fixes that, but only because the sampling happens *outside* the model:

```
~/work/bin/python ~/.claude/skills/rpg-dev/scripts/rolodex.py --from <adventure-dir> npc
~/work/bin/python ~/.claude/skills/rpg-dev/scripts/rolodex.py --from <adventure-dir> location casino
```

Three candidates per slot, sometimes a wildcard. `rpg-dev` calls this during the NPC and
Scene layers, then writes past what the dice put on the table.

## Casting NPC portraits

`rpg-npc-cast` turns an NPC's **Visual** / **Cast** / **Register** notes (written during
`rpg-dev`) into a portrait that looks like a real person under pressure in the setting — not
the cast actor smiling on a red carpet. Run it in a **fresh session**, pointed at the
finished adventure file, so image work doesn't bloat your design context:

```
/rpg-npc-cast cast the NPCs in @dagger-isles/fighting-goats.md
```

It reads each NPC, writes a de-glamorizing prompt, and either calls Gemini directly (needs a
billing-enabled key) or, with `--prep`, hands you the prompt to generate free in the Gemini
app. Portraits land in an `image/` folder next to the adventure file; record each one back
under its NPC as `- **Portrait:** ![Name](image/name.png)`. See the skill's
[SKILL.md](skills/rpg-npc-cast/SKILL.md) for the prompt recipe and the two routes.

## Install

### As a plugin (recommended)

Add this repo as a marketplace, then install the plugin:

```
/plugin marketplace add mburnamfink/rpg-dev-skills
/plugin install rpg-dev-skills
```

### Manually

Copy (or symlink) the skill folders into your global skills directory:

```bash
git clone https://github.com/mburnamfink/rpg-dev-skills.git
cd rpg-dev-skills
mkdir -p "$HOME/.claude/skills"
for s in rpg-dev rpg-npc-cast rpg-critic rpg-revise rpg-publish; do
  ln -sfn "$PWD/skills/$s" "$HOME/.claude/skills/$s"
done
```

Per-project instead of global? Symlink into a project's `.claude/skills/` the same way.

## Dependencies

Two skills need something beyond Claude Code; the rest of the workflow is pure Markdown.

`rpg-publish`'s render step (scripts in `skills/rpg-publish/scripts/`):

- `pdf.sh` — [pandoc](https://pandoc.org/) with a XeLaTeX engine
- `wiki.sh` — [pandoc](https://pandoc.org/) (browsable HTML wiki; no LaTeX needed)
- `gen-cards.py` — Python 3 (pregen character cards: Markdown → HTML)
- `render-cards.sh` — headless Chrome/Chromium (turns the `gen-cards.py` HTML into a one-page PDF)

`rpg-npc-cast`'s portrait step:

- `cast-npc.py` — Python 3 with [`google-genai`](https://pypi.org/project/google-genai/)
  (`pip install google-genai`) and a `GEMINI_API_KEY` from [Google AI Studio](https://aistudio.google.com/apikey)
  on a **billing-enabled** project (image generation has no free API tier). Or use the
  script's free `--prep` mode and generate by hand in the Gemini app.

## License

MIT — see [LICENSE](LICENSE).
