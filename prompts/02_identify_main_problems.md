# Step 2 — Identify Main Problems

**Purpose:** Group the feedback records from Step 1 into the main recurring
problems, each backed by evidence, across all sources.

**How to use:** Don't edit this file. In the **same chat** as Step 1, attach this file and send:

```text
Follow the prompt in the attached 02_identify_main_problems.md. Use only the part below the "---" line. Use your Step 1 answer above as the input.
```

*Tool doesn't support attachments?* Copy everything below the line and paste it as your message, unchanged. The `{{PLACEHOLDERS}}` tell the AI to use its earlier answers.

> **✅ Before you continue to Step 3**
> 1. **Read the review table** at the top of the answer: one row per problem, with its item count and sources.
> 2. **Run the automatic checks:** in the dashboard, click **Check a step** and paste the whole answer. It checks that counts match the listed IDs, that every item appears exactly once, that no IDs were invented, and that every quote is word-for-word.
> 3. **Use your judgment.** In the dashboard, open a few problems to read their items side by side:
>    - Do all items in a problem describe the same failure?
>    - Do the titles describe what goes wrong for customers, not a cause?
>    - Is anything in *Other items* actually part of a problem?
> 4. **If anything is wrong,** copy the fix message the dashboard gives you (or write your own, e.g. *"S-2105 belongs in P4"*), send it in the same chat, and check the corrected answer again.

---

You are a senior customer insights analyst. Using the extracted feedback records,
identify the **main problems** customers are experiencing.

## Ground rules
1. **Feedback is the only evidence.** Every problem must be supported by the records. Use the business context only to understand terms.
2. **No inference, assumption or invention.** Do not merge items because they *might* share a cause. Group by what the feedback actually shows.
3. **Quotes are verbatim** and must come from the records' `key_quotes` or `stated_explanations`.
4. **Count exactly.** Every count must match the listed IDs. Never estimate or round.
5. **Never invent IDs.** Every item from Step 1 must appear exactly once: in one problem or in `other_items`.

## How to group
- A **problem** is something that goes wrong in the customer experience, described from the customer's point of view (e.g. "Couriers wait a long time at stores because orders are not ready"). It is **not** a root cause. Causes come in Step 3.
- Group items that describe the **same failure**, even when they come from different sources or author types. A support ticket, a survey answer and an app review can all describe one problem. Seeing the same problem in several sources is strong evidence that it is real.
- Assign each problem item to exactly **one** problem: the one that best describes its main issue.
- A problem needs **at least 2 items**. Put single-item issues and items with `is_problem: false` in `other_items`.
- Sort problems by `item_count`, highest first. Number them `P1`, `P2`, ...

## Inputs
If an input below still shows a `{{PLACEHOLDER}}`, use the matching material from
earlier in this conversation: the business context for `{{BUSINESS_CONTEXT}}`,
and your complete Step 1 JSON for `{{STEP_1_OUTPUT}}`.

<business_context>
{{BUSINESS_CONTEXT}}
</business_context>

<feedback_records>
{{STEP_1_OUTPUT}}
</feedback_records>

## Output
Return two parts, in this order.

**Part 1 — Review table** (for a person to check quickly):

| Problem | Title | Items | Sources | Author types |
|---|---|---|---|---|

Then one line: *Items in problems: A · Other items: B · Total: A + B (should equal the number of Step 1 records).*

**Part 2 — JSON** in a single ```` ```json ```` code block:

```json
{
  "problems": [
    {
      "id": "P1",
      "title": "Short problem name (max ~8 words)",
      "description": "2–3 sentences describing what goes wrong and who is affected, based only on the feedback.",
      "item_ids": ["T-0000", "S-0001", "R-0002"],
      "item_count": 3,
      "by_source": { "support_ticket": 1, "survey": 1, "app_review": 1 },
      "by_author_type": { "merchant": 1, "courier": 2 },
      "evidence": [
        { "item_id": "T-0000", "source": "support_ticket", "speaker": "courier", "quote": "Exact quote." }
      ]
    }
  ],
  "other_items": [
    { "item_id": "S-0003", "reason": "Single occurrence: <topic>" }
  ]
}
```

- `by_source` and `by_author_type` must each add up to `item_count`.
- `evidence`: include 2–4 quotes per problem, from different sources and author types where possible. Each quote must come from an item in that problem.
