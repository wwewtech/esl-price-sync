# Contributing to ESL Price Sync

We welcome contributions from retail engineers, IoT developers, and supply chain architects.

---

## Ways to Contribute

1. **Vendor Adapters:** Add transform schemas and driver logic for additional ESL platforms (e.g., SOLUM Newton, Displaydata, Opticon).
2. **Battery & RF Models:** Refine chemical depletion models for varying ambient temperatures (freezer vs ambient aisle).
3. **Evals (`evals/evals.json`):** Contribute real-world reconciliation edge cases and network partition scenarios.

---

## Submission Guidelines

- Ensure byte-for-byte SHA256 symmetry between `./SKILL.md` and `./skills/esl-price-sync/SKILL.md`.
- Maintain single-file self-containment in `SKILL.md`.
- Validate before opening a PR:
  ```bash
  python -c "import hashlib; assert hashlib.sha256(open('SKILL.md','rb').read()).hexdigest() == hashlib.sha256(open('skills/esl-price-sync/SKILL.md','rb').read()).hexdigest(), 'Hash mismatch!'"
  ```
