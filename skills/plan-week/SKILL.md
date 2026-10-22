---
name: plan-week
description: Use when the person wants outfits planned for several days, such as a work week, a trip, or a packing list.
---

# Plan the week

There is no single "plan week" tool. Build the plan from the read tools, then save the outfits the person approves.

## Steps

1. Ask what the days look like (office, gym, dinner, travel) unless they already said.
2. Call `wardrobe.summary` once to see what categories they have and which pieces are most and least worn.
3. For each day, call `outfits.suggest` with that day's `occasion`.
4. Avoid repeating any piece more than twice in the week, except basics like jeans or shoes. If a suggestion repeats too much, swap pieces with `wardrobe.search`.
5. Show the week as a short list: day, occasion, pieces.
6. After they approve, save each outfit with `outfits.save` and a name like "Mon – office".
7. On each day, if they confirm they wore it, use `wear.log` with that day's `worn_on`.

## Packing for a trip

Plan the days the same way, then list each piece once with how many days it's used. Pieces that work in three or more outfits are a good sign.

## Don't

- Don't save the whole week in one go without showing it first.
- Don't assume weather. Ask or look it up.
