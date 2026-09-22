# Complete Distribution & Collections Directory

This registry catalogs **`esl-price-sync`** across every AI agent directory, Cursor rule repository, Claude Code showcase, awesome-list, and community distribution channel.

---

## 1. Official Registries & Package Hubs

| Platform | Type | Link / Command | Submission Method | Status |
| :--- | :--- | :--- | :--- | :--- |
| **skills.sh** (Vercel) | Universal CLI Registry | [skills.sh/wwewtech/esl-price-sync](https://skills.sh/wwewtech/esl-price-sync) | Git Tag / Auto-Indexed | Indexed & Verified |
| **Anthropic Official Skills** | Show & Tell Showcase | [Anthropic Skills Forum](https://github.com/anthropics/skills/discussions) | Official Community Forum | Ready to Publish |
| **Cursor Directory** | Cursor Rules Hub | [cursor.directory](https://cursor.directory/) | Form / GitHub PR | Ready to Submit |
| **Awesome Claude** | Claude Code Hub | [awesomeclaude.ai](https://awesomeclaude.ai/) | "Submit Resource" / PR | Ready to Submit |
| **Cline Rules Hub** | Roo Code / Cline Directory | [clinerules.org](https://clinerules.org/) | GitHub PR | Ready to Submit |
| **Smithery.ai** | Agent Capabilities Registry | [smithery.ai](https://smithery.ai/) | Indexed via `smithery.json` | Manifest Configured |
| **Glama.ai** | Agent Tools & MCP Hub | [glama.ai/mcp](https://glama.ai/mcp) | Web Submission | Ready to Submit |

---

## 2. GitHub Awesome-Lists Submissions & PR Tracker (20 Curated Targets)

| Repository | Focus / Category | Status |
| :--- | :--- | :--- |
| **sickn33/agentic-awesome-skills** (46,500+ ⭐) | AAS Core / `skills/esl-price-sync/SKILL.md` | Prepared / Active |
| **ComposioHQ/awesome-claude-skills** (75,000+ ⭐) | `IoT, Retail Tech & Enterprise Integration` | Prepared / Active |
| **heilcheng/awesome-agent-skills** (6,200+ ⭐) | `Retail IoT & Distributed Systems` | Prepared / Active |
| **VoltAgent/awesome-agent-skills** (34,500+ ⭐) | `Community Skills -> IoT & Retail` | Prepared / Active |
| **PatrickJS/awesome-cursorrules** (10,000+ ⭐) | `Retail IoT / Fullstack` (`rules/esl-price-sync.mdc`) | Prepared / Active |
| **BehiSecc/awesome-claude-skills** (10,000+ ⭐) | `Enterprise & IoT Tools` | Prepared / Active |
| **rohitg00/awesome-claude-code-toolkit** (2,300+ ⭐) | `Skills -> IoT & Synchronization` | Prepared / Active |
| **Prat011/awesome-llm-skills** (1,700+ ⭐) | `Retail Systems & IoT Protocols` | Prepared / Active |
| **libukai/awesome-agent-skills** (5,100+ ⭐) | `精选技能 -> 智能零售与物联网 (Smart Retail & IoT)` | Prepared / Active |
| **skillmatic-ai/awesome-agent-skills** (670+ ⭐) | `Popular Collections / Retail Tech` | Prepared / Active |
| **philipbankier/awesome-agent-skills** | `Domain-Specific -> Retail Automation` | Prepared / Active |
| **karanb192/awesome-claude-skills** | `IoT & Retail Systems` | Prepared / Active |
| **spencerpauly/awesome-cursor-skills** | `Enterprise IoT Workflows` | Prepared / Active |
| **jqueryscript/awesome-claude-code** (510+ ⭐) | `Agent Skills -> Enterprise Tools` | Prepared / Active |
| **awesome-iot** | `Retail IoT, BLE & Sub-GHz ESL gateways` | Target Catalog |
| **awesome-retail-tech** | `POS, ERP & Electronic Shelf Label sync` | Target Catalog |
| **awesome-ecommerce** | `Omnichannel price synchronization` | Target Catalog |
| **awesome-embedded** | `Low-power e-paper displays & battery telemetry` | Target Catalog |
| **awesome-distributed-systems** | `Idempotent batch syncing & delta queues` | Target Catalog |
| **awesome-supply-chain** | `In-store inventory & shelf pricing telemetry` | Target Catalog |

---

## 3. High-Traffic Launch Channels

### 1. Hacker News (Show HN)
- **Title:** `Show HN: ESL Price Sync – Agent skill for Electronic Shelf Label IoT pricing pipelines`
- **URL:** `https://wwewtech.github.io/esl-price-sync/`
- **Body:**
  ```text
  Hey HN!

  Retailers deploying Electronic Shelf Labels (SES-imagotag, Pricer, Hanshow, SoluM) frequently suffer from pricing desync between in-store POS databases and physical e-paper tags. In flight RF packet loss or unbatched updates drain ESL lithium coin cells in months instead of 5 years.

  We built esl-price-sync (https://github.com/wwewtech/esl-price-sync), an open-source agent skill (SKILL.md) that governs reliable ESL synchronization:
  1. Idempotent delta queueing (only transmit changed prices/promo flags)
  2. RF transmission batch throttling (preserves e-paper coin-cell battery life)
  3. CRC32 payload verification & ACK reconciliation loops
  4. Battery telemetry alerting (flags coin cells under 2.4V)

  Install via Skills CLI:
  $ npx skills add wwewtech/esl-price-sync
  Or for Claude Code:
  $ claude skills add https://github.com/wwewtech/esl-price-sync

  Live synchronization visualizer: https://wwewtech.github.io/esl-price-sync/
  ```

### 2. Product Hunt
- **Tagline:** `Autonomous IoT synchronization engine for Electronic Shelf Labels`
- **Description:** `An autonomous agent skill for retail tech and IoT developers to synchronize POS/ERP pricing to ESL e-paper tags with delta batching, checksum validation, and battery telemetry.`
- **Tags:** `IoT`, `Retail`, `E-Commerce`, `Developer Tools`, `Open Source`.

### 3. Reddit (`r/retail`, `r/embedded`, `r/sysadmin`, `r/ClaudeAI`)
- **r/retail:** `Eliminating in-store price discrepancies with Electronic Shelf Label (ESL) automated sync pipelines`
- **r/embedded:** `Sub-GHz/BLE Electronic Shelf Label power optimization: batching transmissions to save coin-cell batteries`
- **r/ClaudeAI:** `[Skill] ESL Price Sync: Connect ERP/POS databases to Electronic Shelf Label gateways`

### 4. Russian Tech Ecosystem (Хабр & Telegram)
- **Хабр:** «Электронные ценники (ESL): как синхронизировать 50 000 e-paper дисплеев без потери батареи и расхождений с кассой»
- **Telegram:** `@retail_tech`, `@iot_community`, `@ecommerce_tech`, `@neuro_dev`.

---

## 4. Universal 1-Click Installation Cheatsheet

```bash
# 1. skills.sh (Universal Skills CLI)
npx skills add wwewtech/esl-price-sync

# 2. Claude Code
claude skills add https://github.com/wwewtech/esl-price-sync

# 3. Google Antigravity
curl -sL https://raw.githubusercontent.com/wwewtech/esl-price-sync/main/SKILL.md -o ~/.gemini/config/skills/esl-price-sync/SKILL.md

# 4. Cursor (.cursor/rules/ or .cursor/skills/)
mkdir -p .cursor/skills/esl-price-sync
curl -sL https://raw.githubusercontent.com/wwewtech/esl-price-sync/main/SKILL.md -o .cursor/skills/esl-price-sync/SKILL.md

# 5. Windsurf / Cascade
mkdir -p .windsurf/skills/esl-price-sync
curl -sL https://raw.githubusercontent.com/wwewtech/esl-price-sync/main/SKILL.md -o .windsurf/skills/esl-price-sync/SKILL.md
```
