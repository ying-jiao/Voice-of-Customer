# Business Context — Acme Direct (fictional example)

> Acme Direct is a fictional company created for this example. All feedback items in
> `sample_feedback.csv` are synthetic.

## 1. What the business does
Acme Direct is an on-demand, last-mile delivery platform. Merchants (restaurants,
grocers, pharmacies and retailers) use it to deliver orders placed on the
merchant's **own** website, app or point-of-sale system. Acme Direct provides the
couriers and the delivery logistics; the merchant owns the customer relationship.
Merchants pay Acme Direct a fee per delivery.

## 2. Who gives feedback

| Author type | Who they are | What they typically write about |
|---|---|---|
| Merchant | Business that requests deliveries (paying customer). Includes store staff, owners, finance teams and the developers who build integrations. | Delivery issues, billing questions, integration and account setup help |
| Consumer | Person receiving the delivery. Ordered from the merchant's channel, so may not know Acme Direct by name. | Late, missing or mis-delivered orders |
| Courier | Independent contractor who picks up and delivers orders using the Acme Courier App. | Pay questions, problems at pickup or drop-off |

## 3. How the core flow works
1. **Create delivery:** The merchant creates a delivery through the Merchant Dashboard, the Delivery API, or a third-party POS integration.
2. **Dispatch:** Acme Direct assigns a courier, timed so the courier arrives at the store when the order is expected to be ready.
3. **Pickup:** The courier collects the order at the store.
4. **Drop-off:** The courier navigates to the drop-off address and completes the delivery, following any drop-off instructions.
5. **Return (if undeliverable):** If the delivery cannot be completed, the courier returns the items to the store.

## 4. Key features, fields and terminology

| Term | Meaning |
|---|---|
| Merchant Dashboard | Web portal where merchants manage stores, settings and invoices |
| Delivery API | API merchants or their developers use to create deliveries |
| POS integration | Third-party point-of-sale software connected to the Delivery API |
| Prep time | Store-level setting: expected minutes from order creation until the order is ready |
| `ready_at` | Optional API field: the time a specific order will be ready |
| `dropoff_instructions` | API field: instructions for the courier at the drop-off location |
| `order_notes` | API field: general notes about the order |
| Acme Courier App | Mobile app couriers use to accept, navigate and complete deliveries |
| Wait pay | Extra courier pay for time spent waiting at the store |
| Return | Courier brings an undeliverable order back to the store |
| Invoice | Weekly statement of delivery fees and other charges sent to merchants |
| Earnings summary | Weekly statement of pay shown to couriers in the app |

## 5. Relevant policies
- Wait pay starts after a courier has waited 10 minutes at the store.
- When an order is returned, the merchant is charged a return fee and the courier receives return pay.
- Consumers can receive credits or refunds at the support agent's discretion.

## 6. Feedback sources

| Source | What it is | Notes for reading it |
|---|---|---|
| support_ticket | Conversations between a merchant, consumer or courier and an Acme Direct support agent | Agents often explain how dispatch, billing and pay work |
| survey | Free-text answers from three surveys: the merchant satisfaction survey, the courier pulse survey and the consumer post-delivery survey. The question is in the `title` column. | One answer per response; no follow-up questions |
| app_review | App store reviews of the Acme Courier App | Public; star rating is in the `title` column |

## 7. Analysis scope
- Feedback from 2026-08-03 to 2026-08-12, all sources.
- Goal: identify the main problems and their root causes, and recommend product and operations fixes.
