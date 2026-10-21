# Step 1 — Extract Feedback Facts

**Purpose:** Turn each piece of raw customer feedback into a structured,
evidence-backed record. Feedback can be a support ticket, a survey response, an
app review or a comment. Later steps work from these records instead of
re-reading the raw text.

**How to use:** Don't edit this file. Start a **new chat** in your AI tool, attach **three files** (this file, your business context and your feedback CSV), and send this message with your own file names:

```text
Follow the prompt in the attached 01_extract_feedback_facts.md. Use only the part below the "---" line; the text above it is notes for me. The business context is business_context_acme_direct.md and the feedback is sample_feedback.csv.
```

*Tool doesn't support attachments?* Copy everything below the line, paste it as your message, and replace `{{BUSINESS_CONTEXT}}` and `{{FEEDBACK}}` with the full text of each file. For more than ~40 items, run this step in batches and combine the JSON arrays.

> **✅ Before you continue to Step 2**
> 1. **Read the review summary** at the top of the answer. The record count should equal the number of items in your file.
> 2. **Run the automatic checks:** open `dashboard/index.html`, click **Check a step**, and paste the whole answer. It checks that every item is present, that no IDs were invented, and that every quote is word-for-word.
> 3. **Use your judgment:** are the items marked *not a problem* really just compliments or how-to questions?
> 4. **If anything is wrong,** copy the fix message the dashboard gives you (or write your own), send it in the same chat, and check the corrected answer again.

---

You are a senior customer insights analyst. Your job in this step is to extract
facts from customer feedback. Do not analyze, group or diagnose yet.

## The feedback you will receive
Each item has an `item_id`, a `source`, an `author_type` and its `text`. Sources
differ in what they can tell you:

| Source | What it usually contains | What it can prove |
|---|---|---|
| `support_ticket` | A conversation between the customer and a support agent, with each message prefixed by `[Speaker]` | What happened, and often **why**: agents frequently explain how the system works |
| `survey` | One free-text answer to a survey question (the question is in `title`) | What the respondent experienced and wants; rarely why it happened |
| `app_review`, `comment`, other | One piece of free text from the author | What the author experienced and thinks |

## Ground rules (apply to every field you write)
1. **Feedback is the only evidence.** Every fact must come from the feedback text. The business context explains terminology and how the product works. Never use it as proof that something happened.
2. **No inference, assumption or invention.** Do not guess motives, causes, frequencies or outcomes that are not stated. If information is not in the item, write `null`. Do not fill the gap.
3. **Quotes are verbatim.** Copy quotes character-for-character from the text. Do not paraphrase inside a quote, fix typos or merge sentences from different messages.
4. **Attribute every statement.** Record who said it: the author (merchant, consumer, courier, etc.) or a support agent. An agent's explanation of how the system works counts as evidence of a mechanism. An author's opinion about why something happened is their **claim**, so record it as one.
5. **Never invent IDs.** Use the item IDs exactly as given, and include **every** item.

## Inputs
If an input below still shows a `{{PLACEHOLDER}}`, use the matching file attached
to this message: the business context (`.md`) for `{{BUSINESS_CONTEXT}}` and the
feedback export (`.csv`) for `{{FEEDBACK}}`.

<business_context>
{{BUSINESS_CONTEXT}}
</business_context>

<feedback>
{{FEEDBACK}}
</feedback>

## Output
Return two parts, in this order.

**Part 1 — Review summary** (for a person to check quickly; keep it short):
- Records extracted: N, and the number of items in the input
- Records by source and by author type
- Items marked `is_problem: false`, each with a reason of 10 words or fewer
- Number of items that contain an agent's explanation of a cause

**Part 2 — JSON** in a single ```` ```json ```` code block: an array with one object per item, in this exact shape:

```json
[
  {
    "item_id": "T-0000",
    "source": "support_ticket | survey | app_review | comment | ...",
    "author_type": "merchant | consumer | courier | ...",
    "is_problem": true,
    "issue": "One sentence: what went wrong for the author, in plain words.",
    "facts": [
      "Short factual statement taken from the text."
    ],
    "stated_explanations": [
      {
        "speaker": "agent | merchant | consumer | courier | ...",
        "explanation": "Why the issue happened, as stated by someone in the item.",
        "is_author_claim": false,
        "quote": "Exact supporting quote."
      }
    ],
    "requests": ["What the author asks for or suggests, if anything."],
    "impact_stated": "The consequence for the author as stated, or null.",
    "key_quotes": [
      { "speaker": "merchant | consumer | courier | agent | ...", "quote": "Exact quote." }
    ]
  }
]
```

Field guidance:
- `is_problem`: `false` for compliments, simple how-to questions and requests that involve no failure. Still include these items.
- `stated_explanations`: **only statements about why** the issue happened: a cause or a mechanism, such as an agent saying "your prep time is set to the default of 10 minutes". A description of *what* happened ("the food wasn't ready") is not an explanation; it belongs in `facts`. Set `is_author_claim` to `true` when the author (not an agent) is explaining. Use an empty array if nobody explained the cause. **This field is the main input for root cause analysis, so be exact and complete.**
- `requests`: feature requests and suggestions are useful later as solution evidence. Quote them closely.
- `impact_stated`: the **consequence** for the author (time lost, money, damaged goods, a bad rating, a refund). How often something happens is a fact, not an impact.
- `key_quotes`: 1–3 quotes that best show the problem and its cause.
