# HumaniserUltra

Makes AI text sound human. Not word-swapping — understanding what makes writing human and applying those patterns.

77 detection patterns. 16 hard rules. 11 domain adapters.

## Install

**One command (all harnesses):**
```bash
npx skills add beastboymayu/HumaniserUltra
```

**Per harness:**

| Harness | Command |
|---------|---------|
| Claude Code | `/plugin marketplace add beastboymayu/HumaniserUltra` |
| OpenCode | `npx skills add --agent opencode beastboymayu/HumaniserUltra` |
| Cursor | `npx skills add --agent cursor beastboymayu/HumaniserUltra` |
| Codex | `npx skills add --agent codex beastboymayu/HumaniserUltra` |
| Cline | `npx skills add --agent cline beastboymayu/HumaniserUltra` |
| Windsurf | `npx skills add --agent windsurf beastboymayu/HumaniserUltra` |
| Zed | `npx skills add --agent zed beastboymayu/HumaniserUltra` |
| Copilot | `npx skills add --agent copilot beastboymayu/HumaniserUltra` |

**Manual:**
```bash
# Any harness — copy SKILL.md to the skills directory
mkdir -p .agents/skills/humaniser && cp SKILL.md .agents/skills/humaniser/

# Claude Code
mkdir -p ~/.claude/skills/humaniser && cp SKILL.md ~/.claude/skills/humaniser/

# OpenCode
mkdir -p ~/.config/opencode/skills/humaniser && cp SKILL.md ~/.config/opencode/skills/humaniser/

# Cursor
mkdir -p .cursor/skills/humaniser && cp SKILL.md .cursor/skills/humaniser/
```

## Usage

```
/humaniser
[paste AI text to humanize]
```

**Write from scratch:**
```
/humaniser
Write me an email asking for a raise
```

**Match your voice:**
```
/humaniser
Here's how I write: [paste your writing sample]
Now write this in my voice: [topic]
```

## What It Does

- **5 input gates** — handles short text, non-English, already-human, code blocks, injection vectors
- **16 hard rules** — zero em dashes, no AI vocabulary (47 banned words), no signposting, no sycophancy
- **77 patterns** — content, language, style, structural, spectral, model-specific, detector-specific
- **11 domain adapters** — Academic, Creative, Business, Journalistic, Casual, Legal, Medical, Technical, Creative Writing, Email, Social Media
- **6-pass process** — scan → rewrite → spectral disruption → voice/soul → domain calibration → audit
- **Verification** — grep-based checks, compliance score with every output

## Before / After

**Before:**
> I recently spent five unforgettable days in Lisbon, and let me tell you — this city completely stole my heart. Nestled along the banks of the Tagus River, Lisbon stands as a vibrant testament to Portugal's enduring spirit.

**After:**
> I spent five days in Lisbon last October and still have mixed feelings about it. Beautiful, yes. Also harder on the knees than anyone warned me. The hills are the whole story and somehow never make the brochures.

## File Structure

```
HumaniserUltra/
├── SKILL.md              # The skill
├── README.md             # This file
├── AGENTS.md             # Quick reference for agents
├── LICENSE               # MIT
└── .claude-plugin/
    └── plugin.json       # Claude Code marketplace manifest
```

## Known Limits

Does not defeat: RLHF fingerprint detection, discourse-level persistence, watermarks. For those, combine with cross-model rewriting or back-translation (documented in skill).

## License

MIT
