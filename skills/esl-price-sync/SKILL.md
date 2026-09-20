---
name: esl-price-sync
description: Sync retail prices from ERP/POS to Electronic Shelf Labels (ZKONG, SES-imagotag, Pricer, Hanshow, SOLUM): delta updates, idempotency, rate-limited rollout, promo scheduling, and audit trail. Use when connecting shelf-edge labels to pricing sources, debugging ghost pricing, or planning ESL deployments. Read-only audit mode by default; writes require explicit approval.
---

# ESL Price Sync

Keep shelf-edge prices identical to the ERP price master. Ghost pricing (ERP says one thing, shelf shows another) costs money and trust — this skill makes the sync pipeline correct.

## Scope

- ESL platforms: ZKONG, SES-imagotag, Pricer, Hanshow, SOLUM (vendor specifics differ; principles below are universal).
- Flows: full sync, delta sync, promo scheduling, rollback, audit.
- Out of scope: dynamic-pricing strategy itself (what price to set) — this skill covers faithful delivery of decided prices.

## When NOT to use

- Single-label troubleshooting without system context — check the gateway first.
- E-commerce/website pricing — different stack.

## Method

1. **Map the pipeline.** Identify the five layers: price master (ERP) → middleware/transform → ESL management platform → gateway/base station → label. Record which layer owns formatting, queuing, and retry for this deployment.
2. **Audit mode first (read-only).** Pull a sample of SKUs: compare ERP price vs platform state vs last gateway ACK. Report mismatches with SKU, expected, actual, and layer where they diverge. Change nothing.
3. **Delta discipline.** Never full-catalog push on a schedule: compute changed SKUs since last watermark, push only deltas. Full pushes are for initial load and disaster recovery only.
4. **Idempotency.** Every price command carries an idempotency key (ERP transaction ID). Gateways must dedupe retries — resends must not drain label batteries or double-apply promos.
5. **Rate limiting.** Cap update bursts at ~75-80% of the ESL radio throughput; priority order: compliance fields (unit price, allergens) → promos → regular prices → informational fields. Dead-letter anything failing after retries.
6. **Promo scheduling.** Promotions carry start/end timestamps evaluated at the edge; verify timezone handling (store-local, not UTC-naive) and pre-dawn activation before opening.
7. **Audit trail.** Every label update links back: ERP transaction → transform timestamp → platform ACK → label confirm. Retain per local consumer-protection rules (EU: minimum 2 years).

## Write rules

- No mass price push without explicit approval and a stated rollback (previous price set + re-push plan).
- Never invent SKU prices: every value comes from the ERP/master, quoted with source transaction.
- If a label shows a price the ERP never authorized, treat as incident: quarantine the SKU, investigate, do not silently overwrite.

## Honesty rules

- State which ESL vendor flow was assumed; vendor APIs differ — verify against the deployed platform docs.
- If gateway ACK data is unavailable, mark sync state `unverified`, never `synced`.
