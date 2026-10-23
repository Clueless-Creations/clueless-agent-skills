---
name: weekly-closet-update
description: Use when offering or running a weekly closet intake from chat photos, outfit-post screenshots, social exports, or forwarded order emails. Offer the routine once; create it only after they say yes.
---

# Weekly closet update

Read [AGENTS.md](../../AGENTS.md) method 1 and [closet-import](../closet-import/SKILL.md) first. This is the recurring intake, not the first fill. Personal stylists run a weekly "new in" pass so new pieces are tagged, deduped, and owned before they disappear into a camera roll or inbox.

`skills.index` is **coming**. Do not call it. There is no closet-update scheduler on the connector. Use the host's recurring task (Muse, ChatGPT scheduled task, or the equivalent) only after they say yes.

## Offer once

After the closet already has pieces, offer once:

> Want a weekly closet update from new photos and order emails?

Create the recurring weekly task only if they say yes. If they say no, do not ask again for a while. Do not create it because it would be useful.

## Each run

1. Ask what arrived this week, or work from what they already sent. Do not invent a shopping trip or a calendar. Sources you may use:
   - Photos shared in chat
   - Outfit-post screenshots or a social export they uploaded
   - Forwarded order or shipping emails
2. For every distinct piece you can name, call `wardrobe.search` (query plus canonical `category_group`, for example `bottoms`). Skip anything already there.
3. Confirm ownership before any write. Shared household orders, tagged group photos, and "we" language: ask which pieces are theirs. Do not add someone else's clothes.
4. Add only the confirmed new pieces, with the source that matches how they arrived:
   - Chat photos → `wardrobe.add_pieces` with `source: "muse_chat_photo"`
   - Outfit-post screenshots → `source: "screenshot"`
   - Social exports they uploaded → `source: "social_export"`
   - Things they mention → `source: "chat_mention"`
   - Order emails → `wardrobe.add_items` with one message per line (`retailer`, `orderRef`, `lineRef`, `kind`). Resending the same receipt never duplicates. If lines come back as `needs_confirmation`, ask which are theirs, then resend with `confirmed_line_keys`.
5. Send `brand` or `size` only if a label shows it or they said it. Use the closet's canonical `category_group` values. Do not invent `pants` or `trousers`.
6. Call `wardrobe.summary` again and `signals.list` for unfinished receipt lines.

## Recap (required)

End with a short list. Do not estimate.

- **Added:** each new piece by canonical category (and name if you have it).
- **Skipped:** duplicate (already in search), not theirs, or still unconfirmed.
- **Open:** receipt lines from `signals.list` that still need a yes.

If summary and search counts differ after the add, report both and say whether a merge or filter is the likely cause.

## Don't

- Don't create the weekly task without a yes.
- Don't add a piece you have not searched for.
- Don't add someone else's clothes from a shared order or photo.
- Don't guess brand or size.
- Don't invent a category group the closet does not already use.
- Don't shop or name stores. This run only records what they already have.
- Don't call `skills.index`. It is **coming**.
