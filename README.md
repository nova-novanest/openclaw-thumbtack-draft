# openclaw-thumbtack-draft

A reusable [openclaw](https://github.com/nova-novanest/openclaw-multi-agent-template) skill that drafts replies to inbound Thumbtack leads for solo home service pros — designed to win the conversation in the first 60 seconds.

This is the **methodology layer** behind [Novanest Pro](https://novanestpro.com), my AI system that runs a real US home services business solo from Barcelona. The production system has live API credentials, real prices, and customer-specific tuning that aren't in this repo. **What's in this repo is the structural pattern: how to think about a Thumbtack reply, what wins, and what kills the deal.**

If you're a solo service pro, an AI builder working on lead-conversion tools, or just curious how a multi-agent system handles real customer messages — this is the skill spec.

---

## What's in this repo

| File | Purpose |
|---|---|
| `SKILL.md` | The full skill specification: orchestrator pattern, pricing framework structure, the proven reply formula, hard rules, mid-conversation rules |
| `example_replies.md` | Worked examples of the formula applied to common lead types (sanitized — no real customers) |
| `LICENSE` | MIT |

## What's NOT in this repo

- **Actual prices.** The production system uses task-based pricing tuned to Hovo's specific business and California market. The structure of the framework is in `SKILL.md`, but the numbers are placeholders. Plug in your own.
- **Internal API endpoints / tokens.** Removed.
- **Customer data or specific lead history.** Removed.
- **The Python backend** (FastAPI, SQLite, webhook intake, dispatch pipeline). That's a separate, private codebase. See [novanest-pro](https://github.com/nova-novanest/novanest-pro) for the architecture overview.

---

## Why publish this

I built Novanest Pro by analyzing 100+ real Thumbtack lead conversations and reverse-engineering what made some win and others lose. The pattern isn't proprietary — it's verifiable craft. Any pro who reads this skill spec can apply it manually or wire it into their own system.

The thing that's hard to copy is **doing it consistently in under 60 seconds for every lead, automatically, while you're on the ladder doing the actual work.** That's what the production system handles. The methodology in this skill is what the production system encodes.

---

## Use it as an openclaw skill

If you're running [openclaw](https://github.com/nova-novanest/openclaw-multi-agent-template):

```bash
cd ~/.openclaw/workspace/skills/
git clone https://github.com/nova-novanest/openclaw-thumbtack-draft.git thumbtack-draft
```

The `SKILL.md` frontmatter will be auto-detected. Tune the prices in the pricing table to match your own market, plug in your base location for the travel-surcharge step, and you're ready to draft.

## Use it as a standalone reference

`SKILL.md` is just markdown. You can read it, copy it into your own playbook, or adapt the principles to a totally different lead source (Yelp, Angi, Google Local Services). The orchestrator pattern, the "match the description length" rule, the "answer the literal question first" rule, the "never offer free on-site estimate" rule — none of those depend on Thumbtack specifically. They're generic conversion patterns.

---

## License

[MIT](LICENSE) — use this however you want, including commercially. Attribution appreciated but not required.

---

Built by [Hovhannes Hovhannisyan](https://hovhannes.dev) (Hovo) from Barcelona. Originally extracted from [Novanest Pro](https://novanestpro.com).
