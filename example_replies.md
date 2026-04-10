# Example Replies

Worked examples of the winning formula applied to common Thumbtack lead types. **Customer details are fully fabricated** — these are illustrative examples only, not real lead data.

---

## Example 1 — Single doorbell, customer has hardware

**Inbound (description, 14 words):**

> *I have a Ring doorbell I bought last month. Need someone to install it.*

**Reply (16 words):**

> *Hey Sarah! Just saw your note — sounds like a quick setup. $[price] installed and tested. Tomorrow works. When's good?*

**What it does right:**
- Length match: 14 words in, 16 out ✅
- Price up front ✅
- Acknowledges they have the hardware (*"installed and tested"* = labor only)
- One question, asking WHEN ✅
- Doesn't repeat *"Ring doorbell"* back ✅

---

## Example 2 — Multiple cameras, ambiguous count

**Inbound (28 words):**

> *Looking to install 3-5 cameras around my house. Some on the front, some on the back. Not sure exactly how many yet. Need someone reliable.*

**Reply (32 words):**

> *Hey Mike! Just saw your note — sounds like a quick setup. $[per_unit_price] each, installed and tested. I can stop by Wednesday or Thursday and finalize the count on-site. When works?*

**What it does right:**
- Length match: 28 words in, 32 out ✅
- Per-camera price (no assumption about count, since count is unclear) ✅
- One concrete offer: "Wednesday or Thursday" not "this week" ✅
- "Finalize on-site" preserves their flexibility without offering a free estimate visit ✅
- Single WHEN question ✅

---

## Example 3 — Anxious customer (post-break-in language)

**Inbound (31 words):**

> *Hi, my neighbor's house got broken into last week and we're worried. We need cameras around our property as soon as possible. Can someone help this week please.*

**Reply (37 words):**

> *Hey Jen — totally understand, that situation is stressful. $[price] all in for the full setup, installed and tested before I leave. I can be there tomorrow morning if that works for you. When's good?*

**What it does right:**
- Acknowledges the emotional state ("totally understand, that situation is stressful") — one line, no overdoing it
- Price still up front ✅
- "Installed and tested before I leave" — strong reassurance for the anxious customer ✅
- Concrete time offer: "tomorrow morning" not vague ✅
- One question ✅

**What it does wrong if you over-correct:**
- DO NOT write a long sympathy paragraph. Customers in fear want *action*, not empathy theater.

---

## Example 4 — Customer who replied with a price question

**Conversation so far:**

- Bot: *"Hey Tom! Just saw your note — sounds like a quick setup. $[price] all in. Tomorrow works. When's good?"*
- Customer: *"Is that the final price including the wiring and conduit?"*

**Reply (26 words):**

> *Yes, $[price] covers full wiring and setup — everything safe and working. If you want the wires hidden in conduit covers that's extra, but it's not mandatory. When works this week?*

**What it does right:**
- **Answers the literal question first** ("Yes, $[price] covers...") ✅
- Names the edge case honestly (conduit covers are extra) ✅
- Re-anchors to WHEN ✅
- Doesn't add new information that wasn't asked for ✅

**The wrong reply (anti-pattern):**

> ❌ *Makes sense. When are you free? I'll fit around your schedule.*

This is a documented failure: it skipped the literal price question. The customer asked something specific, and the bot pivoted without answering. The post-send QA pass in the production system catches this exact pattern and ships a corrective reply within minutes.

---

## Example 5 — Cheap lead, low-stakes job

**Inbound (9 words):**

> *Need help setting up 2 wifi cameras. Battery type.*

**Reply (12 words):**

> *Hey Alex — $[low_price] for both, all in. Today or tomorrow?*

**What it does right:**
- Length match: 9 words in, 12 out ✅
- No fluff, matches the casual tone ✅
- Same formula, just compressed ✅

**What to avoid:**
- Don't downgrade your professionalism just because the job is cheap
- Don't pad the message because you feel embarrassed about a low quote

---

## What these examples are NOT

- **Not real customer messages.** Every name, situation, and detail is fabricated.
- **Not a script to copy verbatim.** The formula is the structure; the specifics should match your voice and your market.
- **Not a guarantee.** No reply system wins every lead. The point is to win more of them, more consistently, faster.

---

Built by [Hovhannes Hovhannisyan](https://hovhannes.dev) (Hovo) from Barcelona.
