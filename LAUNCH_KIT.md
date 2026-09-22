# ESL Price Sync — Global Launch & Distribution Kit

This kit contains high-engagement announcement templates to publish and distribute `esl-price-sync` across major retail tech, IoT, and developer communities.

---

## 1. Twitter / X Viral Launch Thread

### Post 1 (Hook + Banner):
> Retailers lose millions on in-store pricing discrepancies and dead Electronic Shelf Label (ESL) batteries.
>
> Pushing 10,000 price updates blindly over sub-GHz radio drains 5-year lithium batteries in 6 months.
>
> Today we're open-sourcing **ESL Price Sync**: an autonomous agent skill for deterministic retail IoT pricing pipelines 🧵👇
>
> `npx skills add wwewtech/esl-price-sync`
> [Attach: assets/esl-banner.svg]

### Post 2 (The IoT Synchronization Problem):
> ESL systems (SES-imagotag, Pricer, Hanshow, SoluM) need careful handling:
> - RF transmission throttling to preserve e-paper coin-cell battery life
> - CRC32 checksum verification to avoid corrupt barcode rendering
> - Delta-only queueing (never re-transmit unchanged prices)
> - Real-time battery telemetry alerts (< 2.4V)

### Post 3 (Enterprise Architecture):
> Connects ERP and Point-of-Sale (POS) databases directly to ESL base stations.
> Handles network partitions, offline queuing, and retry policies gracefully.

### Post 4 (Install & Run):
> 📦 skills.sh: https://skills.sh/wwewtech/esl-price-sync
> ⭐ GitHub: https://github.com/wwewtech/esl-price-sync
> 🌐 Web Visualizer: https://wwewtech.github.io/esl-price-sync/

---

## 2. Reddit (`r/retail`, `r/embedded`, `r/sysadmin`, `r/ClaudeAI`)

### Title:
> **Preventing dead ESL batteries and pricing discrepancies with an open-source agent skill for Electronic Shelf Labels**

### Body:
> Hey everyone,
>
> In retail stores with 30,000+ Electronic Shelf Labels (ESL), price updates are often a headache:
> - Frequent bulk updates drain coin-cell batteries prematurely.
> - Network timeouts leave half the shelf tags showing old promotional prices.
>
> We built **ESL Price Sync** (https://github.com/wwewtech/esl-price-sync), an open-source agent skill (`SKILL.md`) that guides agents in:
> - Implementing delta-only pricing queues with CRC32 checksums
> - Scheduling batched RF transmissions during low-traffic windows
> - Parsing low-battery telemetry and signal strength (RSSI)
> - Verifying audit trails between ERP master records and tag confirmation ACKs
>
> **Install:**
> ```bash
> npx skills add wwewtech/esl-price-sync
> ```
>
> Repo: https://github.com/wwewtech/esl-price-sync
> Interactive Simulator: https://wwewtech.github.io/esl-price-sync/

---

## 3. Pull Request Submission Template

```markdown
## Summary
Adds the `esl-price-sync` skill to `skills/esl-price-sync/SKILL.md`.

### Overview
`esl-price-sync` equips autonomous coding agents with reliable retail IoT synchronization logic for Electronic Shelf Label (ESL) systems, enforcing delta queueing, battery-preserving RF batching, and checksum-verified ACK reconciliation.

### Features
- Idempotent delta queueing to eliminate redundant transmissions
- Battery longevity protection and voltage telemetry monitoring
- CRC32 payload verification for e-paper price displays
- POS/ERP integration presets with offline partition recovery

### Validation
Passes all CI checks with 0 errors and 0 warnings. Verified against canonical price sync evals.
```
