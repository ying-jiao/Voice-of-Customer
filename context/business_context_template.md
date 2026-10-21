# Step 0 — Business Context

> **Why this matters.** The AI has never seen your product. Without context it
> can't tell a merchant from a courier, doesn't know what "prep time" or
> "Adjustment" means, and can't follow a why-chain into how your product works.
>
> **What the AI may and may not do with it.** It uses this context only to
> **understand** your feedback. It is **never** treated as evidence that a
> problem happened; only the feedback itself is evidence.
>
> **How to fill it in.** Replace each `<!-- ... -->` block with your own answer.
> Each section has an example from a fictional meal-kit subscription company,
> *FreshBox*, so you can see the level of detail that works. For a complete
> filled-in version, see [`examples/business_context_acme_direct.md`](../examples/business_context_acme_direct.md).
> Aim for 1–2 pages. Remove anything confidential before pasting it into an AI
> tool your company hasn't approved.

---

# Business Context — <Your Product Name>

## 1. What the business does
<!-- One paragraph: the product, who pays for it, and the core value it delivers. -->

> **Example:** FreshBox is a weekly meal-kit subscription. Customers choose 3–5
> recipes each week in the FreshBox app, and we deliver the ingredients in an
> insulated box on their chosen delivery day. Customers pay per box; they can
> skip weeks or pause their subscription at any time.

| ❌ Too vague | ✅ Useful |
|---|---|
| "We are a food company." | Says who the customer is, what they get, how they pay, and what they can change. |

## 2. Who gives feedback
<!-- Each author type that appears in your feedback, and their relationship to the product.
     Use the same names you'll use in the `author_type` column. -->

| Author type | Who they are | What they typically write about |
|---|---|---|
|  |  |  |

> **Example:**
>
> | Author type | Who they are | What they typically write about |
> |---|---|---|
> | subscriber | Paying customer with an active or paused subscription | Missing ingredients, delivery timing, billing, recipes |
> | delivery_partner | Third-party courier company delivering boxes | Address problems, access to buildings, box volume |

## 3. How the core flow works
<!-- The main lifecycle in numbered steps. Include the moments where things can go wrong. -->

1.
2.
3.

> **Example:**
> 1. **Menu opens:** Every Wednesday, next week's menu is published.
> 2. **Selection cutoff:** Subscribers choose recipes until Sunday 23:59. If they don't choose, we pick for them.
> 3. **Billing:** The box is charged at cutoff, not on delivery.
> 4. **Packing:** Boxes are packed at one of two warehouses.
> 5. **Delivery:** A delivery partner delivers in a 4-hour window on the chosen day.

## 4. Key features, fields and terminology
<!-- Terms that appear in your feedback, including internal names support agents use. -->

| Term | Meaning |
|---|---|
|  |  |

> **Example:**
>
> | Term | Meaning |
> |---|---|
> | Cutoff | Deadline for changing next week's box; also when the box is charged |
> | Skip | Subscriber pauses one week without cancelling |
> | Ice pack exception | Warehouse flag when a box ships without enough ice packs |
> | Credit | Account balance applied to the next box; agents use it to compensate |

## 5. Relevant policies
<!-- Fees, refunds, pay rules, SLAs: anything that appears in feedback or that agents cite. -->

-

> **Example:**
> - Missing ingredients are refunded as credit, not cash, unless the subscriber asks.
> - Boxes are charged at cutoff, even if the subscriber later skips that week.
> - Deliveries outside the 4-hour window qualify for a $10 credit.

## 6. Feedback sources
<!-- Each source you will include, what it is, and anything that affects how to read it.
     Use the same names you'll use in the `source` column. -->

| Source | What it is | Notes for reading it |
|---|---|---|
|  |  |  |

> **Example:**
>
> | Source | What it is | Notes for reading it |
> |---|---|---|
> | support_ticket | Chat and email conversations with support agents | Agents often explain billing and warehouse rules |
> | survey | Answers to "What could we do better?" in the post-delivery survey | One free-text answer per response; no follow-up |
> | app_review | iOS and Android app store reviews | Public and often emotional; may mention several issues at once |

## 7. Analysis scope (optional)
<!-- Date range, sources, regions, or specific questions you want answered. -->

-

> **Example:**
> - Feedback from 1–30 September, all sources, US only.
> - We especially want to understand why missing-ingredient complaints rose in September.
