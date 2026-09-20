# esl-price-sync

Sync retail prices from ERP/POS to Electronic Shelf Labels (ZKONG, SES-imagotag, Pricer, Hanshow, SOLUM): delta updates, idempotency, rate-limited rollout, promo scheduling, and audit trail.

**Install this skill:**
```bash
npx skills add wwewtech/esl-price-sync
```

## Links
- [Live Showcase](https://wwew.tech/esl-price-sync/)
- [skills.sh](https://skills.sh)
- [SKILL.md](SKILL.md)

## Why use this skill?
Keep shelf-edge prices identical to the ERP price master. Ghost pricing (ERP says one thing, shelf shows another) costs money and trust — this skill makes the sync pipeline correct, debugging issues, or planning deployments.

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
curl -sL https://raw.githubusercontent.com/wwewtech/esl-price-sync/main/SKILL.md -o ~/.gemini/config/skills/esl-price-sync/SKILL.md
```

### 4. For Cursor & Windsurf
Add `SKILL.md` to your workspace prompt context:
```bash
mkdir -p .cursor/skills/esl-price-sync
curl -sL https://raw.githubusercontent.com/wwewtech/esl-price-sync/main/SKILL.md -o .cursor/skills/esl-price-sync/SKILL.md
```


## Core Concepts

- **Map the pipeline.** ERP → middleware/transform → ESL management platform → gateway/base station → label.
- **Audit mode first (read-only).** Pull a sample of SKUs and report mismatches. Change nothing.
- **Delta discipline.** Compute changed SKUs since last watermark, push only deltas.
- **Idempotency.** Dedupe retries with ERP transaction IDs.
- **Rate limiting.** Cap update bursts at ~75-80% of the ESL radio throughput.
- **Promo scheduling.** Timezone-aware start/end timestamps evaluated at the edge.
- **Audit trail.** Trace every label update back to the ERP transaction.

## License

MIT © wwewtech
