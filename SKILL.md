---
name: thumbtack-draft
description: >-
  Generates a winning reply to an inbound Thumbtack lead for a solo home
  service pro. Implements the orchestrator + sub-agent pattern, applies a
  task-based pricing framework, and uses a verified "winning formula" reply
  template optimized for under-60-second response times. Use whenever a new
  Thumbtack lead arrives or when responding to a customer mid-conversation.
---

# Thumbtack Draft Generation Skill

A reusable openclaw skill for drafting Thumbtack lead replies that actually convert.

> **Note on prices:** Every dollar amount in this skill is a **placeholder**. The methodology is the value — plug in your own task-based rates from your own market.

---

## Orchestrator Pattern (mandatory)

Your orchestrator (e.g. Claude Opus) is the decider. It does NOT do research itself — it delegates to a sub-agent worker.

**Flow:**

1. **Orchestrator reads the lead** — understand the person, what they need, their emotional state. A few tokens, no tool calls yet.
2. **Spawn a research sub-agent** for location/context lookups. Give it a focused task brief:

   ```
   sub_agent.spawn(task="""
   Research this Thumbtack lead for a reply draft.
     - Customer first name: [name]
     - Location: [city, zip]
     - Category: [category]
     - Description: '[verbatim from lead]'

   Do these lookups and return findings only (no draft):
     1. Drive time from [YOUR_BASE_LOCATION] to [zip]
     2. Neighborhood profile for [zip] — type (suburban/urban/apartments), median home value
     3. Anything notable about the area or customer

   Keep findings under 150 words. Return facts only.
   """)
   ```

3. **Research returns → orchestrator writes the draft** using the intel + the pricing framework + the winning formula below.
4. **Patch the draft** back to wherever your system stores pending replies (e.g. an approval queue, a Telegram message, a webhook callback).

This pattern saves ~80% of orchestrator tokens while keeping draft quality high. **For obvious leads** (e.g. a single doorbell install in a familiar zip), skip the research spawn and draft directly.

---

## Input

The skill receives:

- `customer_name` — first name only is fine
- `location` — city + zip code
- `category` — Thumbtack's category label
- `description` — the verbatim text the customer typed
- `details` — Thumbtack's checkbox/dropdown answers (treat as form noise unless they conflict with the description)
- `lead_price` — what the platform charged you for this lead

---

## Step A — Price the Job

Build a **task-based** pricing table for your own market. The structure looks like this:

| Task | Placeholder Price |
|---|---|
| Camera setup, normal height (Wi-Fi config only) | `$X` |
| Camera setup, ladder needed (15ft+) | `$X + ladder fee` |
| Indoor smart camera (wall mount, app pairing) | `$X` |
| Outdoor wired camera (cable management, clean run) | `$X` |
| Battery camera install (no wiring) | `$X` |
| Floodlight camera (electrical to junction box) | `$X` |
| Smart doorbell (wired existing chime location) | `$X` |
| Smart doorbell (no existing wiring, needs solar or battery) | `$X` |

**Pricing rules:**

- Add up the tasks, no home-value multiplier. **Task cost is task cost.**
- If the customer already owns the hardware (check `details` for the "already have the security features" answer or the equivalent), price labor only — no hardware markup.
- If the camera count is unclear (e.g. "1–2 cameras"), give a per-camera price. Don't assume a count.

**Why task-based and not flat:** Customers comparison-shop on flat quotes. A per-task breakdown anchors the conversation in *what you're doing*, not *what you're charging*. It also lets you price-discriminate honestly per job without negotiating.

---

## Step B — Travel Surcharge (silent)

Run a drive-time lookup from your base location to the customer's zip:

- **Under 45 min** → no surcharge
- **45–75 min** → add a flat surcharge to your total (suggested: small, e.g. ~$25). **Never mention to the customer.** Bake it into the quote.
- **Over 75 min** → larger flat surcharge (suggested: ~$75). Same — silent, baked in.

Mentioning a travel surcharge to a Thumbtack customer is a documented conversion killer. They feel charged for something they don't see value in. Bake it into the price and present a single number.

---

## Step C — Hardware Check

Check `details` for any field that says the customer already has the equipment.

- **They have it** → price labor only
- **They don't** → you can either price labor + hardware-at-cost or labor only and ask them to buy specific products

**Recommendation:** for installs under $400, price labor only and ask the customer to buy the hardware. It's cleaner, you avoid markup negotiation, and you avoid being responsible for the wrong product.

---

## Step D — Read the Description

This is the highest-leverage step. Most pros skip it.

- **Description = the only real input.** It's the only thing the customer actually typed with their own hands.
- **Details/checkboxes = form noise.** They're filtered through Thumbtack's form UI and don't reflect how the customer actually thinks. Use them only to confirm what the description already implies.
- **Count words.** Match the description length in your reply, +/- 30%. If they wrote 8 words, write 10–15. If they wrote 80 words, write 100. Mismatching length is a tone failure customers notice subconsciously.
- **Match vocabulary.** If they write casually, you write casually. If they use technical terms, you use technical terms. Mirror them.
- **Do NOT repeat what they said back to them.** *"So you need cameras installed?"* is the death sentence of an opener. They know what they wrote. They want to know what you're going to do.

---

## Step E — Write the Reply

### The winning formula

```
Hey [Name]! Just saw your note — sounds like a quick setup.
$[price] [installed/all in]. [Today/Tomorrow] works.
When's good?
```

This template was extracted from a sample of historical hired-vs-not-hired leads. It's not magic — it's the structural elements that win:

1. **Greeting + acknowledgment** in one line
2. **Price up front** in dollars, not "starting at"
3. **Concrete availability** today or tomorrow, not "this week"
4. **One question, asking WHEN** (not WHAT)

### Variations

| Situation | Variation |
|---|---|
| Customer already owns hardware | *"You've got the system — $[X] installed and tested. What days work?"* |
| Need one piece of info to price | Ask for **photo OR count** — never both. Then price in the next message. |
| High-stakes / anxious customer | Add one reassurance line: *"installed and tested before I leave."* |
| Low lead price (cheap job) | Same formula, lower price, faster turnaround offer. Don't downgrade tone. |

### Hard rules

- **"Just saw your note — sounds like a quick setup"** — use this verbatim. It tested better than every variation I tried.
- **Give the price in message 1 or 2, always.** *"I'll get you a quote"* is a near-zero conversion phrase.
- **Offer today or tomorrow** — never "this week," never "next week."
- **One question max — and the question is WHEN, not WHAT.** Asking *"what kind of cameras?"* hands the conversation back to the customer's homework. Asking *"when's good?"* moves toward booking.
- **Match description length.** 8 words in → 10–15 words out max. 80 words in → 100 words out.
- **Never offer a free on-site estimate.** Customers who accept free on-site estimates are documented to ghost after the visit at much higher rates than customers who book on a phone quote.
- **"Installed and tested before I leave"** is a strong value signal. Use it on jobs that justify it.
- **Never send two messages before the customer replies.** If your previous outbound has no reply yet, hold.

---

## Mid-Conversation Replies

When the customer has already replied to your first message and you need to respond again, the rules shift slightly:

- **Answer their LITERAL question first** — never skip past it. This is the single most common failure mode of bad reply systems.
- **If they asked about price** → confirm the price clearly (use the same number, no waffling), then ask WHEN.
- **If they asked about what's included** → answer specifically (list what's in, list what's extra if anything), then ask WHEN.
- **If they gave more info** (camera brand, location detail, count) → acknowledge it, confirm or adjust the price, ask WHEN.
- **Never send a non-sequitur.** *"Makes sense. When are you free?"* in response to a price question is a documented failure pattern. You answered nothing.
- **One question max**, always WHEN not WHAT.
- **Match their message length.**
- **Never send a second message before they reply** — if the conversation already has an unanswered outbound from your side, hold.

---

## Implementation notes

This skill is the *methodology layer*. The full Novanest Pro system layers it on top of:

- A FastAPI webhook endpoint that catches Thumbtack v4 lead events
- A SQLite database that persists every lead, message, and approval
- A Telegram pros chat that dispatches the job to a trained local technician
- A post-send QA pass that detects rule violations and ships corrective replies within minutes
- An AI voice fallback (Retell) that calls customers who go silent

None of those pieces are in this repo. They live in the private production codebase. **What's in this repo is the part you can read, learn, and adapt** to your own lead-conversion stack.

---

## License

MIT — use commercially, modify freely, attribution appreciated but not required.

Built by Hovhannes Hovhannisyan (Hovo) from Barcelona, originally extracted from [Novanest Pro](https://novanestpro.com).
