---
name: rpg-npc-cast
description: Generate portrait images for an adventure's NPCs from their casting notes using Gemini 2.5 Flash Image ("Nano Banana"), de-glamorizing the suggested actors so faces fit a stressed, in-period, in-setting character instead of a smiling red-carpet photo. Use when the user wants to cast, illustrate, portrait, or generate images/faces for NPCs in an rpg-dev adventure file, or mentions Nano Banana / Gemini image generation for a module.
---

# RPG NPC Cast — Portraits from casting notes

Turn an NPC's written **Visual** and **Cast** notes into a portrait that looks like a
real person under real pressure in the setting — not the actor smiling on a red carpet.
You write the prompt (the judgment); [scripts/cast-npc.py](scripts/cast-npc.py) does the
mechanical part.

## Two routes

Same prompt recipe and layout either way — pick based on what the user pays for:

- **API route** — the script calls Gemini and files the images automatically. Needs a
  billing-enabled Gemini API project (the free tier's image quota is 0; a consumer Google
  AI Pro/Advanced subscription does **not** grant API access). ~$0.04/image.
- **Prep route (free with AI Pro)** — `--prep` sets up the folders and hands you the prompt;
  you generate in the Gemini app / AI Studio UI (covered by AI Pro), download the image
  into `image/source/`, and `--promote` it to current. No API key, no per-image cost.

## Setup (once)

- Install the SDK (API route only): `uv pip install --python ~/work/bin/python google-genai`
- API route also needs a key from [Google AI Studio](https://aistudio.google.com/apikey)
  on a billing-enabled project: `export GEMINI_API_KEY=...` (also accepts `GOOGLE_API_KEY`).
- Prep route needs neither.

## Layout

`cast-npc.py` owns a per-adventure folder so the current face is always one grab from the top:

```
<adventure-dir>/image/
    <npc>.png            current portrait (latest generation, auto-promoted)
    source/
        <npc>-v1.png …   superseded portraits and extra variants
        <actor>.jpg      reference images you drop in for -r
```

The script creates `image/` and `image/source/` on every run. `--npc "Tilda Merrick"`
slugifies to `tilda-merrick`. Put reference images under `image/source/` yourself.

## Workflow

1. **Locate** the adventure file and the NPC(s) to cast. Read each NPC's
   Role/Wants/Secret/Voice/**Visual**/**Cast**, and the **Premise** for period and place.
2. **Write the prompt** per NPC using the recipe below. Confirm one prompt with the user
   before generating the whole cast — the house look should be agreed first.
3. **Generate** — one of:
   - *API route:*
     ```
     ~/work/bin/python <skill>/scripts/cast-npc.py -a <adventure-dir-or-.md> \
         --npc "Tilda Merrick" -n 3 -p "<prompt>"
     ```
     The first image becomes current `image/<npc>.png` (any prior current archived to
     `source/` as `-vN`); extra variants (`-n 3`) land in `source/` to choose from.
   - *Prep route:* add `--prep` (drop `-n`) — saves the prompt to
     `image/source/<npc>.prompt.txt` and prints it. Paste into the Gemini app, download the
     result into `image/source/`, then promote it (step 4).
4. **Review** the images with the user; iterate on the prompt and regenerate, or promote a
   variant/download: `cast-npc.py -a <dir> --npc "Tilda Merrick" --promote tilda-merrick-v2.png`.
   A refusal exits with code 2 and prints what the model said.
5. **Record** the portrait under the NPC, e.g. `- **Portrait:** ![Tilda](image/tilda-merrick.png)`.

## The prompt recipe

Build each prompt from these clauses, in order. The first clause is the **house look** —
keep it identical across every NPC in a module so the cast reads as one production.

1. **Medium / house look** — e.g. *"Candid 35mm film photograph, muted desaturated color,
   soft available light, grain, shallow depth of field."* Agree this once, reuse it.
2. **Subject + age + likeness** — describe the *features* implied by the cast actor at the
   right age ("a slight, sharp-featured woman of about 19, heart-shaped face, wide-set pale
   eyes"). You may add "in the vein of a young <actor>" as a cue, but expect the model to
   sometimes refuse a named celebrity — if it does, drop the name and keep the description.
3. **De-glamorize** — *no smile, no makeup glam, no studio/red-carpet lighting;* natural
   skin, tired, unposed.
4. **Register** — if rpg-dev gives the NPC a **Register**, use that emotion directly (most
   NPCs have a fixed one at introduction — Tilda is always frightened, Anselm always
   threatening). Otherwise derive the direction from their **Stance**:
   - *Sympathetic* → the register **pulls the player in**: need, warmth under strain, appeal
     (Tilda's fear).
   - *Antagonistic* → it **pushes or threatens**: menace, appetite, cold contempt (Anselm's
     patient hunger).
   - *Ambiguous* → it **withholds**: a face you can't read, an unsettling calm that could
     break either way.

   Either way, render **one** emotion, at **full intensity**, pinned to a
   **specific physical tell** (the eyes + a held stillness: "eyes fixed past the camera, jaw
   tight, braced — the feeling lives there and nowhere else"), never a list. Two failure
   modes: *stacking* signifiers averages into generic "sad"; *diluting* to "a faint
   undercurrent" washes the character into a pretty blank. Focus, not volume. Iterate by
   re-aiming this one clause.
5. **Period + costume** — from the Visual line and the Premise's era.
6. **Environment** — the light and place where the players meet them (dim curio shop, warm
   lamplight, deep shadows).
7. **Framing** — *head-and-shoulders portrait, single subject.* For a physically imposing
   NPC, see Scale below — the default framing will erase their size.

### Scale (imposing NPCs)

Left alone, the model returns a centered, eye-level, headroom-above medium shot that
**neutralizes size** — a 6'4" enforcer comes out as an ordinary bloke. When the threat is
physical, override the framing clause: shoot from a **low angle looking up**, let them
**loom and overfill the frame with the crown cropped**, press neck and shoulders against the
edges, add slight wide-lens foreshortening. Avoid seated or leaning-on-forearms poses — they
shrink the subject and read as harmless.

See [RECIPE.md](RECIPE.md) for a full worked example (Tilda) and the reference-image (`-r`)
restyle mode.

## Notes

- One subject per image; generate supporting NPCs separately, not as a group shot.
- Keep the house-look clause byte-identical across the cast for visual cohesion.
- `cast-npc.py` is a thin wrapper: model default `gemini-2.5-flash-image`, override with
  `--model`. Filenames come from `--npc`; you never pass an output path.
- `--aspect 2:3` (or any of 1:1, 3:2, 3:4, 4:3, 4:5, 5:4, 9:16, 16:9, 21:9) sets the output
  shape through the API, not the prompt text, and overrides a `-r` reference's shape — an
  approved square plate plus a "reproduce exactly, extend the scene to a tall frame" prompt
  comes back as the same plate in the new shape. Every result is checked against the
  requested ratio and a mismatch prints a WARNING. Use it whenever `art_style.md` asks for
  a non-square plate.
