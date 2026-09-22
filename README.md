# esl-price-sync

Autonomous Retail Shelf-Edge Pricing Architecture Specialist for AI coding agents (Claude Code, Cursor, Antigravity, Windsurf).

Synchronizes retail price masters (ERP/POS) to Electronic Shelf Label (ESL) tag fleets (SES-imagotag, ZKONG, Pricer, Hanshow, SOLUM) with SHA256 delta watermarking, monotonic idempotency tokens, and Sub-GHz RF battery preservation models.

```bash
npx skills add wwewtech/esl-price-sync
```

**[Live Showcase & Pipeline Simulator](https://wwewtech.github.io/esl-price-sync/)** • **[skills.sh](https://skills.sh/wwewtech/esl-price-sync)** • **[SKILL.md](SKILL.md)** • **[GitHub](https://github.com/wwewtech/esl-price-sync)**

---

![esl-price-sync banner](assets/esl-price-sync-banner.svg)

---

## Why ESL Price Sync?

Ghost pricing—where the price at the POS checkout scanner differs from the price displayed on the digital shelf edge—costs retailers millions in consumer protection fines, margin leakage, and lost shopper trust. When developers integrate electronic tags using naive REST loops, their pipelines break down in production:

- **Scheduled Full Catalog Floods**: Blasting entire 50,000-SKU store catalogs every midnight, jamming RF gateways for hours and draining coin cell batteries within 8 months.
- **Ghost Price Blindness**: Mistaking an HTTP `200 OK` from the central server REST API as proof that the physical e-paper display on aisle 4 has refreshed (ignoring dropped Sub-GHz wireless packets).
- **Non-Idempotent Retries**: Retrying failed sync calls without deterministic idempotency tokens, generating duplicated queue tasks and packet collisions.
- **Silent Template Canvas Overflow**: Pushing a 6-digit promotional price into a 4-digit template field, truncating the final digit on screen ($19.99 becomes $19).
- **Destructive Rollback Omission**: Launching weekend promotional flash sales without caching the prior baseline price state, requiring frantic manual re-entry when sales conclude.
- **Peak Hour RF Jamming**: Scheduling bulk price updates during Saturday afternoon shopping hours, where mobile customer traffic degrades Sub-GHz and 2.4GHz RF packet reception.

`esl-price-sync` replaces these failure modes with strict delta watermarking ($\Delta$), monotonic versioning, rate-limited gateway batching ($\le 150\text{ tags/min/AP}$), 5-layer ACK traceability, and CR2450 coin cell battery budget modeling.

---

## Transformation in Action

### Before: Dangerous Scheduled Full-Push Loop
```python
# Blasting entire 60,000-SKU store catalog every midnight
for item in database.get_all_products():
    esl_api.post("/tags/update", item)  # RF Channel jam!
# Blind to whether the physical tag actually updated
print("Pushed all prices to server!")
```

### After: Production Idempotent Delta Synchronizer
```python
# Stream incoming updates and evaluate cryptographic row hashes
for item in incoming_catalog_stream:
    current_hash = sha256_watermark(item)
    # Filter strictly changed records
    if current_hash != last_pushed_hashes.get(item.sku):
        idempotency_key = uuidv5_token(item.sku, item.version, current_hash)
        queue_rate_limited_rf(item, idempotency_key, max_rate_per_min=150)

# Verify 5-layer physical tag delivery confirmation
await confirm_gateway_ack(trace_id, timeout_sec=60)
cache_rollback_state(item.sku, previous_price=item.base_price)
```

---

## Quick Installation

### 1. Via `skills.sh` / Vercel Skills CLI
```bash
npx skills add wwewtech/esl-price-sync
```

### 2. Via Claude Code
```bash
claude skills add https://github.com/wwewtech/esl-price-sync
```

### 3. For Google Antigravity
Clone or copy `SKILL.md` directly into your Antigravity skills directory:
```bash
# Windows
mkdir -p "$HOME\.gemini\config\skills\esl-price-sync"
curl -sL https://raw.githubusercontent.com/wwewtech/esl-price-sync/main/SKILL.md -o "$HOME\.gemini\config\skills\esl-price-sync\SKILL.md"

# macOS / Linux
mkdir -p ~/.gemini/config/skills/esl-price-sync
curl -sL https://raw.githubusercontent.com/wwewtech/esl-price-sync/main/SKILL.md -o ~/.gemini/config/skills/esl-price-sync\SKILL.md
```

### 4. For Cursor & Windsurf
Add `SKILL.md` to your workspace prompt context:
```bash
mkdir -p .cursor/skills/esl-price-sync
curl -sL https://raw.githubusercontent.com/wwewtech/esl-price-sync/main/SKILL.md -o .cursor/skills/esl-price-sync/SKILL.md
```

---

## The 10 Banned Anti-Patterns

| Anti-Pattern | Manifestation in Naive Pipelines | Mandatory Production Counter-Rule |
| :--- | :--- | :--- |
| **Scheduled Full Catalog Floods** | Blasting 50k SKUs every midnight. | Stream strict deltas using SHA256 content watermarks. |
| **Ghost Price Blindness** | Assuming API 200 OK = physical display updated. | Require gateway ACK receipts (`status: ACK_CONFIRMED`). |
| **Non-Idempotent Retries** | Retrying without mutation tokens. | Attach `UUIDv5(sku, store_id, price_timestamp)`. |
| **Timezone Ambiguity** | Pushing promo prices without UTC offsets. | Enforce ISO 8601 UTC with explicit local store offsets. |
| **Gateway RF Flooding** | Blasting 5,000 updates/sec to one AP. | Leaky-bucket rate limiting ($\le 150\text{ tags/min/AP}$). |
| **Silent Canvas Overflow** | 6-digit price overflow truncating digits. | Verify bounding box dimensions before enqueueing. |
| **Destructive Rollback Omission** | Launching flash sales without revert cache. | Cache previous active state for 1-click atomic rollback. |
| **Orphan Tag Neglect** | Leaving dead tags in active sync queues. | Flag missing heartbeat tags after 72 hours as `ORPHAN`. |
| **Mid-Day Peak Syncing** | Triggering mass catalog sync on Saturday rush. | Schedule bulk updates during off-peak morning hours. |
| **Unshielded Write Broadcasts** | Writing updates without simulation. | Enforce dry-run simulation mode before live RF dispatch. |

---

## Core Mental Models & Axioms

1. **The 5-Layer ESL Architecture Pipeline**:
   $\text{ERP Master} \to \text{Transform/Middleware} \to \text{ESL Central Server} \to \text{Wireless Base Station} \to \text{Physical Tag}$.
   Every price event carries a persistent `trace_id` verified through to the final physical RF packet receipt.
2. **Cryptographic Delta Watermarking**: Never push unchanged catalog rows. Queue records only when `hash(price, promo_price, unit, barcode) != last_hash`.
3. **The 3-Update Daily Rule & Battery Longevity**: Limiting refreshes to $\le 3$ updates/day guarantees 5.5 to 7 years on dual-CR2450 coin cells.
4. **Gateway Rate-Limiting**: Queue dispatches at $\le 150$ tag updates per minute per access point to prevent RF packet collision storms.
5. **Read-Only Audit Mode**: All diagnostic executions default to non-destructive inspection mode.

---

## Production Archetypes & Presets

### Archetype 1: Idempotent Delta Synchronizer (Python)
```python
def filter_deltas(incoming_feed: list, watermark_cache: dict) -> list:
    to_push = []
    for item in incoming_feed:
        h = hashlib.sha256(f"{item['sku']}:{item['price']}:{item['promo']}".encode()).hexdigest()
        if h != watermark_cache.get(item['sku']):
            to_push.append({**item, "idempotency_key": hashlib.sha1(f"{item['sku']}:{h}".encode()).hexdigest(), "hash": h})
    return to_push
```

### Archetype 2: Battery Longevity Estimation Model
```python
def calculate_tag_lifespan_years(updates_per_day: float, ambient_celsius: float = 20.0) -> float:
    nominal_mah = 1200.0  # Dual CR2450
    temp_derate = 0.65 if ambient_celsius < 0.0 else (0.85 if ambient_celsius < 10.0 else 1.0)
    usable_mah = nominal_mah * 0.85 * temp_derate
    daily_drain_mah = ((updates_per_day * 18.0) + (1.2 * 24.0)) / 1000.0
    return round(usable_mah / daily_drain_mah / 365.25, 2)
```

---

## The 7-Axis Pre-Emit Quality Gate

| Axis | Metric | Target Threshold |
| :--- | :--- | :--- |
| **1. Delta Discipline** | Unchanged catalog filtering | 100% hash-filtered (0 full floods) |
| **2. Physical Traceability** | Delivery verification | Gateway ACK receipt confirmed |
| **3. Idempotency Proof** | Duplicate protection | UUIDv5 token on every mutation |
| **4. RF Gateway Health** | Dispatch queue rate | $\le 150\text{ tags/min}$ per Access Point |
| **5. Battery Longevity** | Daily refresh budget | $\le 3$ updates/day ($> 5\text{ yr}$ lifespan) |
| **6. Layout Protection** | Font canvas overflow | Zero numeric text clipping |
| **7. Rollback Safety** | Promotion revert state | Pre-computed atomic rollback payload |

---

## Collections & Ecosystem Inclusion

`esl-price-sync` is packaged according to the open Agent Skills specification:
- **[skills.sh Directory](https://skills.sh/wwewtech/esl-price-sync)**: Categorized under Retail Tech, Supply Chain, and Enterprise IoT.
- **Anthropic & Claude Code**: Native support via `claude skills add`.
- **Google Antigravity**: Seamless multi-agent workflow integration.
- **Cursor & Windsurf**: Supported through `.cursorrules` and `.windsurfrules`.

---

## License

MIT © [wwewtech](https://github.com/wwewtech)
