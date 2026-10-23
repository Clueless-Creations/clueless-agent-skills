# Clueless agent skills

Instructions for personal assistants (Muse, Grok Bot, ChatGPT, Claude and others) that use the Clueless connector to work with a person's real closet.

Start with [`AGENTS.md`](AGENTS.md). It is the main skill: the methods (closet audit, occasion and weather, fit and color, formulas, wear and cost-per-wear, editing, gap-only shopping lists, week plans) and the connector tools that carry them out. Clueless is the system of record. Sibling skills below are the playbooks for one job.

This repo holds instructions only. There is no backend code and no keys.

Install from this public repo with `npx skills add Clueless-Creations/clueless-agent-skills`.

## Skills

| Skill | What it does |
| --- | --- |
| [AGENTS.md](AGENTS.md) | Methods, checklists, decision rules, and routing for every connected assistant |
| [clueless-daily](skills/clueless-daily/SKILL.md) | Daily playbook: today's outfit, a week or trip, a weekly review, an outfit card, and logging what they wore |
| [compose-outfit](skills/compose-outfit/SKILL.md) | Pick one occasion-true outfit from clothes the person owns, then save it if they like it |
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

The daily playbook uses only this shipped list. Dedicated tools for richer day context, outfit feedback, a saved week plan, and a rendered card are **coming**. Skills must not invent those names. A generated tool reference from the connector's tool list is not in this repo.

## Ground rules for every skill

- Follow [`AGENTS.md`](AGENTS.md). Call the named tool before you state a closet fact.
- Only use item ids that came back from the connector. Never invent ids, brands or sizes.
- Use canonical `category_group` values (for example `bottoms`). The server may also normalize aliases.
- When summary and search counts differ, report both and explain the merge or filter. Do not guess a number.
- Occasion first: never dress them in swimwear or other off-occasion pieces because those pieces are new or unworn.
- Search before you add, so the closet doesn't fill with duplicates.
- Ask before saving, removing or disconnecting anything.
- Some features need a paid Clueless plan. If a tool returns an entitlement error, say so plainly and don't retry.

## License

MIT. See [LICENSE](LICENSE).
