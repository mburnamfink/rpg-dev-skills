# RPG NPC Cast — worked example & reference-image mode

Companion to [SKILL.md](SKILL.md). The prompt recipe, the register/stance rules, and the
scale note live there; this file holds one full worked prompt and the image-to-image path.

## Worked example (Tilda, the frightened witness)

Note the single register at full intensity, pinned to the eyes and a braced stillness — not
a pile of emotions, and not washed out to a calm blank.

> Candid 35mm film photograph, muted desaturated color, soft window light, grain, shallow
> focus. Head-and-shoulders portrait of a slight, sharp-featured woman of about 19 —
> heart-shaped face, wide-set pale eyes, small delicate features (in the vein of a young
> Carey Mulligan), a blunt mod fringe dyed black. No makeup, no smile, unposed. One clear
> register — quiet dread: she stares fixedly past the camera, eyes held wide and unblinking,
> jaw tight, shoulders drawn up, as if listening for footsteps. Not crying, not composed —
> braced; the fear lives in her eyes and her stillness, nowhere else. An oversized cream
> fisherman's jumper; she holds a worn leather shop ledger against her chest; bitten nails.
> Behind her the dim, cluttered interior of a 1960s curio shop, warm lamplight, deep
> shadows. Not glamorous.

## Reference-image mode (stronger likeness)

Drop the photo — an actor headshot or a film still — into `image/source/`, then pass it
with `-r` to restyle it instead of generating from scratch. Repeat `-r` for several
references. Write the prompt as an *edit*: keep the face, change everything else (age it,
add the stress, the period costume, the setting, the film-stock look).

```
~/work/bin/python <skill>/scripts/cast-npc.py -a <adventure-dir> --npc "Tilda Merrick" \
    -r <adventure-dir>/image/source/mckenzie.jpg -p "Keep this face. Restyle as: <clauses 1,3–7>"
```
