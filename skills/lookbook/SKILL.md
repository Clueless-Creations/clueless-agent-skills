---
name: lookbook
description: Use as the default way to show an outfit. Builds a flat-lay or ghost-mannequin grid from owned item references, then checks each tile against the real piece before showing it.
---

# Lookbook (default visual)

Read [AGENTS.md](../../AGENTS.md) method 5 first. After the outfit is occasion-true and complete, this is how you show it. A simple text card is [outfit-card](../outfit-card/SKILL.md) only when they ask for text or you cannot place images.

A lookbook is a product-photography page. Fashion editors and e-commerce teams use it so a buyer can identify the SKU at a glance. The job is identification, not a mood board. A generic "green polo and white sneakers" render fails that job.

A rendered-card tool and `skills.index` are **coming**. Compose the page from `wardrobe.get_item` and the reference order below. Do not invent those tool names or call them.

## Template (fixed)

Use this page every time. Do not restyle it.

- **Grid:** flat-lay (overhead, one plane) or ghost-mannequin (worn 3D shape, no visible body). One method for the whole page. Do not mix.
- **Background:** one neutral (light grey or off-white). No lifestyle set, no second color.
- **Light:** one soft even key, same direction on every tile. No mixed color temperatures.
- **Scale:** shared. A polo is not larger than the pants.
- **Labels:** under each tile, brand, model, and colorway from the item. If a field is missing, write `unknown`. Do not invent a brand or model.
- **Title:** the outfit name or occasion at the top.

Tile order follows the formula: outerwear, top or dress, bottoms (skip if dress), shoes, accessories.

## Reference order (per item)

Ground truth first. Call `wardrobe.get_item` for every id in the outfit.

1. The Clueless item photo or retailer image on that record.
2. If that photo is missing or unreadable, search for the official brand product image with **brand + model + colorway** from the item. Use the brand's own product shot. Do not use a street-style photo of someone else.
3. If both are missing, write a description from the item fields (`name`, `color`, `category_group`, `brand`) and generate from that text only.

Never generate first and judge later. Never describe or generate a garment they do not own.

## Fidelity check (required, every tile)

Put the render beside the reference at a size you can read. Check in this order. One fail is a fail.

| Check | Pass | Fail |
| --- | --- | --- |
| Silhouette and cut | Same outline, length, and fit. Loose stays loose. | A similar garment. Slimmed, cropped, or reshaped. |
| Exact color | Same hue, depth, and colorway under the page light. | Shifted hue or saturation. Cream that became white. |
| Pattern or stripe structure | Same motif, scale, direction, and weave. Jacquard is woven, not printed. | Solid instead of stripe. Wrong repeat or a graphic print. |
| Logo and branding placement | Same mark, size, and place. | Missing, moved, or another brand's mark. |
| Details | Sole, hardware, collar, buttons, and placket match. | Generic sneaker sole, wrong buckle, missing buttons. |

If any check fails, regenerate **once** from the same reference. If it still fails, put the real photo (step 1, or step 2) in that tile. Do not keep a pretty mismatch.

## Label honestly

Every tile says **photo** or **render**. A render is never "their polo." If you fell back to the real photo, say so.

## On-body (optional)

The default page is the flat-lay or ghost-mannequin grid. On-body only when they asked for it, sent their own reference photos, and said you may use those photos.

Then check identity against *those* references: face, build, skin tone, hair. Same person, not a lookalike.

Never use another person's face, a scraped social photo, or a celebrity stand-in. No consent → no on-body. Failed identity check → drop on-body and keep the lookbook grid.

## Worked example

Outfit: green jacquard stripe polo, cream loose pants, brown belt, Reebok Club C 85.

1. Confirm the set with `outfits.suggest` or the ids they chose. Call `wardrobe.get_item` on each id. Read name, color, brand, model, category, and any photo.
2. Build the titled grid, one tile per piece, ghost-mannequin or flat-lay, shared light and scale.
3. Resolve each reference, then run the check:

| Piece | Reference | What a generic render gets wrong | Action |
| --- | --- | --- | --- |
| Green jacquard stripe polo | Item photo, or official polo shot from brand + model + colorway | Solid jersey. Printed rugby stripe. Wrong collar or placket. | Fail pattern and details. Regenerate once from the woven stripe. Still off → real photo. |
| Cream loose pants | Item photo, or official bottoms shot | Slim chino. White instead of cream. Tapered leg. | Fail silhouette and color. Regenerate once. Still off → real photo. |
| Brown belt | Item photo, or official belt shot | Wrong buckle metal or shape. Black strap. | Fail details. Regenerate once. Still off → real photo. |
| Reebok Club C 85 | Item photo, or official Club C 85 colorway | Generic white sneaker. Stan Smith heel tab. Wrong side mark or sole. | Fail logo and sole. Regenerate once from the Club C 85 product shot. Still off → real photo. |

4. Show the page. Label each tile photo or render. Example title: "Jacquard polo, cream loose pants."
5. Ask before `outfits.save`. Do not treat the lookbook as a wear.

A generic "green polo, cream pants, brown belt, white sneakers" picture is a failed lookbook even if the vibe is close.

## Don't

- Don't generate before you have a reference from `wardrobe.get_item` or the official brand search.
- Don't present a render as a photo of their clothes.
- Don't use someone else's face or a scraped image.
- Don't invent brand, model, or colorway to fill a label.
- Don't put an off-occasion piece on the page to fill a tile.
- Don't call `skills.index` or a rendered-card tool. Both are **coming**.
