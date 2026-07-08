# rpg-dev-skills

A set of [Claude Code](https://claude.com/claude-code) skills for building tabletop RPG
adventures — from blank page to table-ready packet. They're system-agnostic: use them for
Blades in the Dark, Lancer, D&D, or anything else.

| Skill | What it does |
|-------|--------------|
| **rpg-dev** | Collaboratively develop an adventure — premise, NPCs, scenes — into one durable Markdown file. |
| **rpg-critic** | Give a finished module a sharp, table-focused critical read and capture it as a critique-and-response log. |
| **rpg-revise** | Fold a human-answered critique back into the module, applying the fixes you accepted. |
| **rpg-publish** | Condense a revised adventure into a tight, dual-audience, publish-ready document, and render it to PDF / wiki. |

The natural loop: **dev → critic → (answer the critique) → revise → publish.**

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
for s in rpg-dev rpg-critic rpg-revise rpg-publish; do
  ln -s "$PWD/rpg-dev-skills/skills/$s" "$HOME/.claude/skills/$s"
done
```

Per-project instead of global? Symlink into a project's `.claude/skills/` the same way.

## Dependencies

Only `rpg-publish`'s render step needs anything beyond Claude Code:

- `scripts/pdf.sh` — [pandoc](https://pandoc.org/) with a XeLaTeX engine
- `scripts/render-cards.sh` — headless Chrome/Chromium

The rest of the workflow is pure Markdown and needs nothing.

## License

MIT — see [LICENSE](LICENSE).
