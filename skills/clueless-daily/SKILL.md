---
name: clueless-daily
description: Use when the person asks what to wear, wants a daily closet routine, plans a week or trip and packing list, asks for a weekly review or lookbook, mentions their closet, or says they wore something. Follows AGENTS.md methods and sibling skills. Uses only tools the connector already lists.
---

# Daily closet routine

Read [AGENTS.md](../../AGENTS.md) first. This file is the day's playbook. For the details of one job, follow the sibling skill. Use only tool names from this repo's README. If a tool is not listed there, do not guess a name or call it.

Dress them from clothes they own by running the AGENTS.md methods with the tools below. Do not skip a required call and guess.

## Rules

- Suggest only pieces they own. Every item id comes from a connector result.
- Never describe or generate a garment they do not own. Name the owned pieces, then show them with [lookbook](../lookbook/SKILL.md). Use [outfit-card](../outfit-card/SKILL.md) only for a text card.
- Never invent brands or sizes.
- Do not shop, name stores, or send them to buy anything. Closet gaps are categories, not products.
- If they named an occasion (office, dinner, rain), pass it. Do not invent calendar details.
- Occasion first. Never put swimwear, sleepwear, or gym-only pieces in a work, dinner, or everyday look because they are new or unworn. Least-worn is a tie-breaker among occasion-true pieces.
- Use canonical `category_group` values (for example `bottoms`). The server may also normalize aliases. Still send the canonical group.
- When `wardrobe.summary` and `wardrobe.search` counts differ, report both and explain the merge or filter. Do not guess a number.
- Neither `today.brief` nor `outfits.suggest` checks the weather. If weather matters, look it up yourself and swap pieces with `wardrobe.search`.
- Choosing an outfit is a plan, not a wear. Call `wear.log` only when they say they wore it.
- Ask before `outfits.save`, `wear.log`, or any add, remove, or disconnect.

## First use

1. Call `wardrobe.summary`. Reconcile any count they ask about with `wardrobe.search` (AGENTS.md method 1).
2. If the closet is thin (under about 15 items), follow [closet-import](../closet-import/SKILL.md). Start with a closet import from order emails or photos they shared, with their OK. A closet sync from another app is only from a file they exported themselves.
3. Collect occasion, schedule, weather, and season (AGENTS.md method 2). Then end the first session with today's outfit (below).
4. If they are not yet linked to their Clueless account, they can open the app and give you the one-time code from **Clueless > Connect to Muse**, then call `connector.link_account`.

## Morning: what to wear today

Follow [compose-outfit](../compose-outfit/SKILL.md). Run AGENTS.md methods 2 and 5.

1. If they named an occasion, call `outfits.suggest` with `occasion`. For a plain "what should I wear today", call `today.brief`.
2. Drop any suggested piece that fails the occasion. Replace it with `wardrobe.search`. Check weather and swap layers the same way.
3. Show the top outfit and, if you have one, an alternate. Each must be a complete formula (top or dress, bottoms unless dress, shoes, outerwear if the weather needs it). Say why in one line from tool data, such as a piece worn least among the occasion-true options. The default visual is [lookbook](../lookbook/SKILL.md).
4. If they want a change, search for an alternative with `wardrobe.search`. Use only ids from the connector.
5. When they approve, offer to save it with `outfits.save`.
6. If they say they wore it, log it with `wear.log`.

Once the closet has about 15 or more items, offer once: "Want me to pick an outfit every weekday morning?" Set up a recurring task only if they say yes. If they say no, do not ask again for a while.

Also offer once, after the closet already has pieces: "Want a weekly closet update from new photos and order emails?" Follow [weekly-closet-update](../weekly-closet-update/SKILL.md). Create that routine only if they say yes.

## Plan a week or a trip

Follow [plan-week](../plan-week/SKILL.md) and AGENTS.md method 9. A saved week-plan tool is **coming**. Build the plan from `wardrobe.summary` and `outfits.suggest`, then save the outfits they approve.

## Lookbook (default visual)

Follow [lookbook](../lookbook/SKILL.md). A rendered-card tool and `skills.index` are **coming**. Compose a flat-lay or ghost-mannequin grid from `wardrobe.get_item` and official brand product images. Run the fidelity check. Label each tile photo or render. Use [outfit-card](../outfit-card/SKILL.md) only when they ask for a text card or you cannot place images.

## Weekly review

Run AGENTS.md methods 1, 4, 6, and 7.

1. Call `wardrobe.summary` for counts and which pieces are most and least worn. If they ask "how many X", reconcile with `wardrobe.search` and explain any merge.
2. Call `insights.gaps` and report category gaps, not stores or brands.
3. Call `insights.cost_per_wear`. If it returns an entitlement error or is not ready, say so and skip it.
4. Build an edit list: keep, tailor, donate, or resell. Ask before `wardrobe.remove_item`.
5. Suggest one outfit built around a piece worn least *that still fits a named occasion*, using `outfits.suggest` or `wardrobe.search`.

## Logging

- "I wore X" with no suggested outfit: find the items with `wardrobe.search`, then call `wear.log`.
- "I bought X": follow [closet-import](../closet-import/SKILL.md). Search first so you do not add duplicates. Use the canonical `category_group`.
- Recurring weekly new-in: follow [weekly-closet-update](../weekly-closet-update/SKILL.md). Offer once; create the routine only after they say yes.

## Don't

- Don't add pieces they don't own.
- Don't save or log without a yes.
- Don't treat "that looks good" as a wear.
- Don't call a tool that is not in the README's shipped list.
- Don't put off-occasion pieces in a look to use something new.
- Don't invent a closet count when tools disagree.

## Coming

Richer day context, outfit feedback (liked / skipped / why), a saved week plan, a rendered outfit card, and `skills.index` are **coming**. Do not invent names for them. Keep using the steps above until the README lists new tools.

## Example

> **Person:** What should I wear today? I have a client lunch and it's raining.
> **Assistant:** calls `outfits.suggest` with `{"occasion": "client lunch"}` because they named an occasion, then checks the weather separately. Drops any suggested swim or gym piece. Swaps in a rain layer from `wardrobe.search`.
> "Rain all day. How about the navy blazer, grey merino crewneck, olive chinos and brown Chelsea boots? You haven't worn the blazer in a while. Backup: the charcoal overshirt look. Want me to save the first one?"
