---
name: outfit-card
description: Use when the person wants to see an outfit laid out, share it, or keep a picture of it.
---

# Render an outfit card

The connector returns outfit data (item ids, names, category groups, colors). It does not return a finished image. Your assistant draws the card from that data.

## Steps

1. Get the outfit: from `outfits.suggest`, `today.brief`, or a list of item ids the person chose.
2. For each piece, call `wardrobe.get_item` for its name, category, color and brand when known.
3. Lay out the card: top to bottom (outerwear, top, bottom, shoes, accessories), one tile per piece.
4. Each tile shows the piece's photo if it has one. If not, show a color swatch with the piece's name. If you use a generated picture, label it clearly as generated.
5. Add a title (the outfit name or occasion) and, if useful, a one-line note.
6. Show it to the person. Ask before saving the outfit with `outfits.save`.

## Simple text version

When you can't render images, use a text card:

```
Gallery night
- Cream silk shirt
- Black wide-leg trousers
- Brown leather loafers
```

## Don't

- Don't show a brand or size the closet doesn't have.
- Don't present a generated picture as a real photo of their clothes.
