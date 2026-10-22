---
name: compose-outfit
description: Use when the person asks what to wear, wants an outfit for an occasion, or asks you to put something together from their closet.
---

# Compose an outfit

## Steps

1. If they named an occasion ("dinner", "office", "rainy commute"), call `outfits.suggest` with `occasion`. For a plain "what should I wear today", call `today.brief`.
2. Both return owned items and favor the pieces worn least. Neither checks the weather. If weather matters, get it yourself and swap pieces using `wardrobe.search` (by `query` or `category`).
3. Show the outfit with each piece's name. Say why in one line, such as "you haven't worn the green cardigan in a while".
4. If they want a change, search for an alternative and show the new set. Use only ids from the connector.
5. When they approve, offer to save it with `outfits.save` (`item_ids`, optional `name`). An outfit needs two or more items, or one dress.
6. If they say they wore it, log it with `wear.log` (`item_ids`, optional `worn_on` date).

## Don't

- Don't add pieces they don't own. If something is missing, say so, and use `insights.gaps` if they want to know what their closet lacks. Don't recommend a store.
- Don't save or log without a yes.

## Example

> **Person:** What should I wear to a gallery opening Friday?
> **Assistant:** calls `outfits.suggest` with `{"occasion": "gallery opening"}` and gets back a black wide-leg trouser, a cream silk shirt and loafers.
> "How about the black wide-leg trousers, cream silk shirt and loafers? You haven't worn the shirt this month. Want me to save it as 'Gallery night'?"
