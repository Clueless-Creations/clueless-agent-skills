---
name: plan-week
description: Use when the person wants outfits planned for several days, such as a work week, a trip, or a packing list. Builds one occasion-true formula per day from owned pieces.
---

# Plan the week

Read [AGENTS.md](../../AGENTS.md) methods 2, 5, and 9 first. A saved week-plan tool is **coming**. Build the plan from the read tools, then save the outfits the person approves.

## Steps

1. Ask what the days look like (office, gym, dinner, travel) unless they already said. Collect weather and season for the span. Do not invent a calendar.
2. Call `wardrobe.summary` once to see what categories they have and which pieces are most and least worn. Use canonical groups (for example `bottoms`). If they ask for a count, reconcile with `wardrobe.search` and explain any merge instead of guessing.
3. For each day, call `outfits.suggest` with that day's `occasion`.
4. Occasion first on every day. Drop swimwear or other off-occasion pieces even if they are new. Complete the formula (top or dress, bottoms unless dress, shoes, outerwear if weather needs it). Swap with `wardrobe.search`.
5. Avoid repeating any piece more than twice in the week, except basics like jeans or shoes. If a suggestion repeats too much, swap pieces with `wardrobe.search`.
6. Show the week as a short list: day, occasion, pieces.
7. After they approve, save each outfit with `outfits.save` and a name like "Mon – office".
8. On each day, if they confirm they wore it, use `wear.log` with that day's `worn_on`.

## Packing for a trip

Plan the days the same way, then list each piece once with how many days it's used. Pieces that work in three or more outfits are a good sign.

## Don't

- Don't save the whole week in one go without showing it first.
- Don't assume weather. Ask or look it up.
- Don't reuse an off-occasion piece to avoid buying or to "use something new".
