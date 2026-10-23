---
name: compose-outfit
description: Use when the person asks what to wear, wants an outfit for an occasion, or asks you to put something together from their closet. Occasion first, then a complete formula from owned pieces.
---

# Compose an outfit

Read [AGENTS.md](../../AGENTS.md) methods 2, 3, and 5 first. This file is the one-outfit loop.

## Steps

1. Collect occasion, schedule, weather, and season. If they named an occasion ("dinner", "office", "rainy commute"), call `outfits.suggest` with `occasion`. For a plain "what should I wear today", call `today.brief`, then still ask what the day holds if that is missing.
2. Both tools return owned items and favor the pieces worn least. Neither checks the weather. Look weather up yourself. Occasion first: drop swimwear, sleepwear, or gym-only pieces from a work, dinner, or everyday look even if they are new or least worn. Replace dropped slots with `wardrobe.search` (by `query` or canonical `category`, for example `bottoms`).
3. Check the formula is complete: top or dress, bottoms unless it is a dress, shoes, and outerwear if weather needs a layer. Size and color come from the items, not from an invented body type.
4. Show the outfit with each piece's name. Say why in one line from tool data, such as "you haven't worn the green cardigan in a while" — only if that piece already fits the occasion. The default visual is [lookbook](../lookbook/SKILL.md).
5. If they want a change, search for an alternative and show the new set. Use only ids from the connector.
6. When they approve, offer to save it with `outfits.save` (`item_ids`, optional `name`). An outfit needs two or more items, or one dress.
7. If they say they wore it, log it with `wear.log` (`item_ids`, optional `worn_on` date).

## Don't

- Don't add pieces they don't own. If something is missing, say so, and use `insights.gaps` if they want to know what their closet lacks. Don't recommend a store.
- Don't save or log without a yes.
- Don't fill a slot with an off-occasion piece because it is new or unworn.

## Example

> **Person:** What should I wear to a gallery opening Friday?
> **Assistant:** calls `outfits.suggest` with `{"occasion": "gallery opening"}` and gets back a black wide-leg trouser, a cream silk shirt and loafers. Checks the set is a complete formula and that no piece is swim or gym-only.
> "How about the black wide-leg trousers, cream silk shirt and loafers? You haven't worn the shirt this month. Want me to save it as 'Gallery night'?"
