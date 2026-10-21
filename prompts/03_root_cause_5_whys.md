# Step 3 — Root Cause Analysis (5 Whys)

**Purpose:** For each main problem, use the 5 Whys to trace it back to a root
cause: something the company controls, which points to a specific product or
operations change.

**How to use:** Don't edit this file. In the **same chat** as Steps 1–2, attach this file and send:

```text
Follow the prompt in the attached 03_root_cause_5_whys.md. Use only the part below the "---" line. Use your Step 1 and Step 2 answers above as the input.
```

*Tool doesn't support attachments?* Copy everything below the line and paste it as your message, unchanged. The `{{PLACEHOLDERS}}` tell the AI to use its earlier answers.

> **✅ Before you continue to Step 4**
> 1. **Read the review table** at the top of the answer: one row per problem, with its root cause, status and confidence.
> 2. **Run the automatic checks:** in the dashboard, click **Check a step** and paste the whole answer. It checks that every problem has a why-chain, that every link has evidence, that every quote is word-for-word, and that chains which stop early are marked *needs investigation*.
> 3. **Use your judgment.** For each root cause, ask the three tests:
>    - Is it a **cause**, not a restatement of the problem?
>    - Is it something the **company controls** (product, policy, process, communication), not just customer behavior?
>    - Does it point to a **specific change**?
> 4. **If anything is wrong,** copy the fix message the dashboard gives you (or write your own, e.g. *"P2's root cause is a symptom; go one why deeper"*), send it in the same chat, and check the corrected answer again.

---

You are a senior customer insights analyst performing root cause analysis using
the **5 Whys** framework.

## Ground rules
1. **Feedback is the only evidence.** Every "because" in a why-chain must be supported by a verbatim quote from the feedback.
2. **Weigh evidence by what it can prove.**
   - A **support agent's explanation** of how the system works is the strongest evidence of a mechanism.
   - An **author's statement** (in a ticket, survey, review or comment) proves what they experienced. Their explanation of *why* is a claim. It can support a link, but it lowers confidence unless other items corroborate it.
   - The **same point made independently in several sources** is stronger than many items from one source.
3. **The business context can explain how something works, but cannot prove that it happened.** You may cite it as `{"type": "business_context"}` to explain a mechanism. At least one feedback quote must also show that this mechanism caused the problem in practice.
4. **No inference, assumption or invention.** If you cannot answer the next "why" with evidence, **stop the chain there.** Do not guess. A shorter chain that is true is better than five links that are invented.
5. **Quotes are verbatim**, with the correct item ID.

## How to run the 5 Whys
For each problem from Step 2:
1. Start with the problem statement.
2. Ask "Why does this happen?" and answer it using evidence. The answer becomes the next statement.
3. Repeat. Stop when you reach the root cause or run out of evidence. This often takes fewer than 5 whys.

## What counts as a root cause
A root cause must pass **all three tests**:
- **Not the symptom:** It is not a restatement of the problem. For example, "couriers arrive too early" is a symptom, not a root cause.
- **Within the company's control:** It is a product behavior, system design, policy, process or communication gap that the company owns. Customer behavior on its own (e.g. "the merchant entered the wrong value") is not a root cause. Ask why the product allowed or encouraged it.
- **Actionable:** Fixing it would clearly point to a specific product or operations change that would prevent the problem from recurring.

If the evidence runs out before a cause passes all three tests, set
`"status": "needs_investigation"`. Write the deepest cause you *can* support
as `root_cause`, and list the open questions that would need data beyond the
feedback to answer.

## Confidence
- `high`: every link is supported by multiple items, including at least one agent explanation of the mechanism.
- `medium`: every link is supported, but some links rest on a single item or only on author statements.
- `low`: the chain stopped early (`needs_investigation`).

## Inputs
If an input below still shows a `{{PLACEHOLDER}}`, use the matching material from
earlier in this conversation: the business context for `{{BUSINESS_CONTEXT}}`,
your complete Step 1 JSON for `{{STEP_1_OUTPUT}}`, and your complete Step 2 JSON
for `{{STEP_2_OUTPUT}}`.

<business_context>
{{BUSINESS_CONTEXT}}
</business_context>

<feedback_records>
{{STEP_1_OUTPUT}}
</feedback_records>

<problems>
{{STEP_2_OUTPUT}}
</problems>

## Output
Return two parts, in this order.

**Part 1 — Review table** (for a person to check quickly):

| Problem | Root cause (one sentence) | Status | Confidence | Number of whys |
|---|---|---|---|---|

**Part 2 — JSON** in a single ```` ```json ```` code block:

```json
{
  "root_causes": [
    {
      "problem_id": "P1",
      "five_whys": [
        {
          "why": "Why do <problem>?",
          "because": "Answer supported by evidence.",
          "evidence": [
            { "type": "quote", "item_id": "T-0000", "quote": "Exact quote." },
            { "type": "business_context", "note": "What the context says about the mechanism." }
          ]
        }
      ],
      "root_cause": "One or two sentences naming the root cause.",
      "category": "product | operations | product_and_operations",
      "status": "confirmed | needs_investigation",
      "confidence": "high | medium | low",
      "confidence_reason": "One sentence explaining the confidence level.",
      "open_questions": ["Data that would confirm or size the cause. Required when needs_investigation; optional otherwise."]
    }
  ]
}
```
