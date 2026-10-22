# Clueless agent skills

Instructions and examples for personal assistants (Muse, Grok Bot, Claude and others) that use the Clueless connector to work with a person's real closet.

Clueless keeps a person's clothes, outfits and wear history. The connector lets an assistant they've connected read that closet and, with their permission, add to it. These skills show how to do common jobs well: pick an outfit, plan a week, make an outfit card to share, and bring a closet over from photos, receipts or another app's export.

This repo holds instructions only. There is no backend code and no keys.

## Skills

| Skill | What it does |
| --- | --- |
| [compose-outfit](skills/compose-outfit/SKILL.md) | Pick one outfit from clothes the person owns, then save it if they like it |
| [plan-week](skills/plan-week/SKILL.md) | Plan five to seven outfits without repeating pieces too often |
| [outfit-card](skills/outfit-card/SKILL.md) | Turn an outfit into a simple card to show or share |
| [closet-import](skills/closet-import/SKILL.md) | Fill the closet from chat photos, order emails, or a file the person exported |

## Getting connected

1. Add the Clueless connector in your assistant (it appears as "Clueless").
2. The person signs in. If they already use the Clueless app, they link their closet with the one-time code from **Clueless > Connect to Muse** (`connector.link_account`).
3. Reading the closet needs the `wardrobe.read` scope. Adding or changing anything needs `wardrobe.write`.

## Tools at a glance

Read: `start_closet_setup`, `wardrobe.search`, `wardrobe.summary`, `wardrobe.get_item`, `outfits.suggest`, `today.brief`, `insights.cost_per_wear`, `insights.gaps`, `shopping.check_item`, `signals.list`, `account.welcome`, `connector.setup_link`

Write: `wardrobe.add_items`, `wardrobe.add_pieces`, `wardrobe.update_item`, `wear.log`, `outfits.save`, `signals.record`, `account.link`, `connector.link_account`

Destructive (only when the person asks): `wardrobe.remove_item`, `connector.revoke`

## Ground rules for every skill

- Only use item ids that came back from the connector. Never invent ids, brands or sizes.
- Search before you add, so the closet doesn't fill with duplicates.
- Ask before saving, removing or disconnecting anything.
- Some features need a paid Clueless plan. If a tool returns an entitlement error, say so plainly and don't retry.

## License

MIT. See [LICENSE](LICENSE).
