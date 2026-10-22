---
name: closet-import
description: Use when the person wants to build or fill in their closet from photos, things they mention, order emails, or a data export from another app or social account.
---

# Closet import

## Start

Call `start_closet_setup`. It returns what's already in the closet and a short checklist of sources. Work through one source at a time.

## Before every add

Call `wardrobe.search` and only send pieces that aren't there yet. Likely duplicates get merged onto the existing item, but searching first keeps things clean.

## Sources

**Photos shared in chat.** Tag every distinct piece you can see. Call `wardrobe.add_pieces` with `source: "muse_chat_photo"` and one entry per piece: `name`, `category_group`, `color`. Add `brand` or `size` only if a label shows it or the person says it.

**Things they mention.** "I just bought a navy peacoat." Use `wardrobe.add_pieces` with `source: "chat_mention"`.

**Screenshots.** Use `source: "screenshot"`.

**Instagram or Facebook data export.** The person downloads their own export and uploads it to you. Pick out clothing they're wearing and use `source: "social_export"`.

**Order and shipping emails.** Use `wardrobe.add_items` with one message per order line (`retailer`, `orderRef`, `lineRef`, `kind`). Resending the same receipt never duplicates. Returns remove the piece, and exchanges keep the final size. If lines come back as `needs_confirmation`, ask the person which are theirs, then resend with `confirmed_line_keys`.

**Another closet app.** Only use a file the person exported from that app themselves. Read it and add pieces with `wardrobe.add_pieces`. Never sign in to another app for them or read its website.

## After

Call `wardrobe.summary` and tell them what was added by category. `signals.list` shows finished receipt imports and pieces still to confirm.

## Don't

- Don't guess brand or size.
- Don't add someone else's clothes from a shared household order.
