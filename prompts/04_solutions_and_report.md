# Step 4 — Potential Solutions & Final Report

**Purpose:** Propose product and operations solutions for each root cause, then
assemble everything into one JSON report that the dashboard
(`dashboard/index.html`) displays.

**How to use:** Don't edit this file. In the **same chat** as Steps 1–3, attach this file and send:

```text
Follow the prompt in the attached 04_solutions_and_report.md. Use only the part below the "---" line. Use your Step 2 and Step 3 answers above as the input.
```

*Tool doesn't support attachments?* Copy everything below the line and paste it as your message, unchanged. The `{{PLACEHOLDERS}}` tell the AI to use its earlier answers.

**The answer is JSON only. That's expected:** the AI doesn't build the dashboard. You paste this answer into `dashboard/index.html`, which checks it and turns it into the report.

> **✅ Check the final report**
> 1. Open `dashboard/index.html`, click **Check a step**, and paste the whole answer. The dashboard recognizes the final report, runs the checks from the earlier steps plus summary and solution checks, and then shows the finished report.
> 2. Click **Verify quotes** and choose your feedback CSV, if you haven't already.
> 3. **Use your judgment:** does each solution fix the root cause, not just the symptom? Does the summary say only what the report shows?
> 4. **If anything is wrong,** send the fix message in the same chat and check the corrected report again.

---

You are a senior customer insights analyst. Propose solutions for each root
cause, then compile the final report.

## Ground rules
1. **Solutions must target the root cause, not the symptom.** For example, "give couriers more wait pay" treats a symptom. "Let merchants signal when an order is ready" removes a cause. For each solution, say which link in the why-chain it breaks.
2. **No invented numbers.** Do not invent costs, timelines, percentages or projected impact. Describe expected effects qualitatively and tie them to the evidence (e.g. "would address the 13 items in P1").
3. **Stay within the evidence.** Do not propose fixes for problems that are not in the analysis. For root causes with `status: "needs_investigation"`, propose **investigation steps** and at most one interim mitigation. Do not propose a full fix for a cause that has not been confirmed.
4. **Customer requests are input, not answers.** When authors asked for something specific (the `requests` field in Step 1), you may cite it as support for a solution with its item ID, but only if it addresses the root cause.
5. **Separate product and operations.**
   - *Product* solutions change the software: features, UI, API, defaults, validation or data.
   - *Operations* solutions change people and processes: onboarding, documentation, support macros, outreach, policies or monitoring.
   Include both types when both apply.
6. **Summary is facts only.** The summary must only restate findings already in the report.

## Inputs
If an input below still shows a `{{PLACEHOLDER}}`, use the matching material from
earlier in this conversation: the business context for `{{BUSINESS_CONTEXT}}`,
your complete Step 2 JSON for `{{STEP_2_OUTPUT}}`, and your complete Step 3 JSON
for `{{STEP_3_OUTPUT}}`.

<business_context>
{{BUSINESS_CONTEXT}}
</business_context>

<problems>
{{STEP_2_OUTPUT}}
</problems>

<root_causes>
{{STEP_3_OUTPUT}}
</root_causes>

## Output
Return the final report JSON below in a single ```` ```json ```` code block. Copy `problems`, `other_items` and
`root_causes` from the earlier steps **unchanged**, then add `meta`, `summary`
and `solutions`.

```json
{
  "meta": {
    "title": "Customer Feedback Root Cause Analysis",
    "product": "Product name from business context",
    "period": "Date range of the feedback, e.g. 2026-08-03 to 2026-08-12",
    "items_analyzed": 0,
    "by_source": { "support_ticket": 0, "survey": 0, "app_review": 0 },
    "by_author_type": { "merchant": 0, "consumer": 0, "courier": 0 }
  },
  "summary": {
    "headline": "One sentence: the single most important finding.",
    "key_findings": [
      "3–6 bullets. Each names a problem, its item count, the sources it appears in and its root cause."
    ]
  },
  "problems": [ "...copied from Step 2..." ],
  "other_items": [ "...copied from Step 2..." ],
  "root_causes": [ "...copied from Step 3..." ],
  "solutions": [
    {
      "problem_id": "P1",
      "product": [
        {
          "title": "Short solution name",
          "description": "What to build or change, in 1–2 sentences.",
          "addresses": "Which why-link this breaks, e.g. 'Why 3: stores rely on a single default prep time'.",
          "requested_in": ["S-0001"]
        }
      ],
      "operations": [
        { "title": "...", "description": "...", "addresses": "...", "requested_in": [] }
      ]
    }
  ]
}
```

Before returning, check that:
- every `item_id` in the report appears in the input,
- `by_source` and `by_author_type` in `meta` each add up to `items_analyzed`,
- the items in `problems` plus `other_items` add up to `items_analyzed`, with no item listed twice,
- every number in `summary` matches the counts in `problems` (recount them; don't recall them),
- every problem has a matching entry in `root_causes` and `solutions`.

After the code block, add exactly one line:
*Next: copy this whole answer, open `dashboard/index.html`, click "✓ Check a step" and paste it. When the checks pass, click "View the report".*
