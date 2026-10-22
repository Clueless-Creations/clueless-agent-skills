---
name: clueless-daily
description: Use when the person asks what to wear, wants a daily closet routine, plans a week or trip and packing list, asks for a weekly review or outfit card, mentions their closet, or says they wore something. Follows the sibling skills and uses only tools the connector already lists.
---

# Daily closet routine

This is the playbook for a day with the person's real closet. For the details of one job, follow the sibling skill. Use only tool names from this repo's README. If a tool is not listed there, do not guess a name or call it.

## Rules

- Suggest only pieces they own. Every item id comes from a connector result.
- Never describe or generate a garment they do not own. Name the owned pieces, or make a card with [outfit-card](../outfit-card/SKILL.md).
- Never invent brands or sizes.
- Do not shop, name stores, or send them to buy anything. Closet gaps are categories, not products.
- If they named an occasion (office, dinner, rain), pass it. Do not invent calendar details.
- Neither `today.brief` nor `outfits.suggest` checks the weather. If weather matters, look it up yourself and swap pieces with `wardrobe.search`.
- Choosing an outfit is a plan, not a wear. Call `wear.log` only when they say they wore it.
- Ask before `outfits.save`, `wear.log`, or any add, remove, or disconnect.

## First use

1. Call `wardrobe.summary`.
2. If the closet is thin (under about 15 items), follow [closet-import](../closet-import/SKILL.md). Start with a closet import from order emails or photos they shared, with their OK. A closet sync from another app is only from a file they exported themselves.
3. End the first session with today's outfit (below).
4. If they are not yet linked to their Clueless account, they can open the app and give you the one-time code from **Clueless > Connect to Muse**, then call `connector.link_account`.

## Morning: what to wear today

Follow [compose-outfit](../compose-outfit/SKILL.md).

1. If they named an occasion, call `outfits.suggest` with `occasion`. For a plain "what should I wear today", call `today.brief`.
2. Show the top outfit and, if you have one, an alternate. Say why in one line, such as a piece worn least.
3. If they want a change, search for an alternative with `wardrobe.search`. Use only ids from the connector.
4. When they approve, offer to save it with `outfits.save`.
5. If they say they wore it, log it with `wear.log`.

Once the closet has about 15 or more items, offer once: "Want me to pick an outfit every weekday morning?" Set up a recurring task only if they say yes. If they say no, do not ask again for a while.

## Plan a week or a trip

Follow [plan-week](../plan-week/SKILL.md). There is no single week-plan tool yet. Build the plan from `wardrobe.summary` and `outfits.suggest`, then save the outfits they approve.

## Outfit card

Follow [outfit-card](../outfit-card/SKILL.md). The connector does not return a finished image. Draw the card from item names, colors, and the person's own photos or a color swatch. Never use a retailer image. Never present a generated picture as a real photo of their clothes.

## Weekly review

1. Call `wardrobe.summary` for counts and which pieces are most and least worn.
2. Call `insights.gaps` and report category gaps, not stores or brands.
3. Call `insights.cost_per_wear`. If it returns an entitlement error or is not ready, say so and skip it.
4. Suggest one outfit built around a piece worn least, using `outfits.suggest` or `wardrobe.search`.

## Logging

- "I wore X" with no suggested outfit: find the items with `wardrobe.search`, then call `wear.log`.
- "I bought X": follow [closet-import](../closet-import/SKILL.md). Search first so you do not add duplicates.

## Don't

- Don't add pieces they don't own.
- Don't save or log without a yes.
- Don't treat "that looks good" as a wear.
- Don't call a tool that is not in the README's shipped list.

## Not on the connector yet

A later connector release is meant to add dedicated tools for richer day context, outfit feedback (liked / skipped / why), a saved week plan, and a rendered outfit card. Those tools are not in the shipped list. Do not invent names for them. Keep using the steps above until the README lists new tools.

## Example

> **Person:** What should I wear today? I have a client lunch and it's raining.
> **Assistant:** calls `outfits.suggest` with `{"occasion": "client lunch"}` because they named an occasion, then checks the weather separately.
> "Rain all day. How about the navy blazer, grey merino crewneck, olive chinos and brown Chelsea boots? You haven't worn the blazer in a while. Backup: the charcoal overshirt look. Want me to save the first one?"
