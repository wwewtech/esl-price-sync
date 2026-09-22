# Changelog

All notable changes to the `esl-price-sync` skill will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.0.0] - 2026-09-22

### Initial Release — Enterprise ESL Pricing Architecture

#### Added
- **Master Skill (`SKILL.md`):** Complete architectural standard for shelf-edge pricing integration.
- **5-Layer Traceability Pipeline:** Trace ID management from ERP to physical tag RF ACK.
- **Cryptographic Delta Watermarking:** SHA256 content hashing to filter unchanged catalog rows.
- **Sub-GHz Gateway Rate-Limiting:** Enforced $\le 150\text{ tags/min/AP}$ dispatch queue protection.
- **CR2450 Battery Longevity Model:** Temperature-dependent capacity de-rating and 3-update daily budget.
- **Interactive Simulator (`docs/index.html`):** In-browser 5-layer pipeline and 3-color e-paper renderer.
- **CI Validation:** Automated YAML frontmatter and SHA256 file symmetry verification.
