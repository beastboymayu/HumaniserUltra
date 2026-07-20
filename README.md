# HumaniserUltra

Makes AI text sound human. Not word-swapping — understanding what makes writing human and applying those patterns.

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

## What This Skill Does Well

**Removes obvious AI tells:**
- Zero em dashes, en dashes (the biggest single signal)
- 47 banned AI vocabulary words (delve, tapestry, pivotal, robust, etc.)
- No signposting ("Let's dive in"), no sycophancy ("Great question!")
- No rule-of-three forcing, no hedged assertions, no curly quotes

**Adds genuine voice:**
- Personality and soul — opinions, uncertainty, first-person perspective
- Register shifts — formal → colloquial transitions mid-paragraph
- Structural roughness — tangents, self-corrections, abrupt endings
- Specificity injection — replace "research shows" with named sources

**Covers 12 domains:**
- Academic (passive voice preserved in Methods), Creative, Business, Journalistic
- Casual/Social Media (platform-native), Legal (terms of art preserved), Medical
- Technical, Creative Writing, Grant Proposals, Resumes/CVs, Multi-Domain

**Handles edge cases:**
- 6 input gates: short text, non-English, already-human, code blocks, tables, injection vectors
- Voice calibration from writing samples
- Long document chunking with voice bible for consistency
- Mixed human/AI text — rewrites transition points, matches human fingerprint

**Provides escalation paths:**
- Base model pipeline (highest-leverage — reads as human to detectors)
- OOD shifting (50x better than pattern elimination against adversarial detectors)
- Detector feedback loop (iterative rewriting with detector scores)
- Back-translation pipeline (EN→ZH→JA→FI→EN chain)

**Verification built in:**
- Compliance score with every output
- Mechanical burstiness checks (longest - shortest ≥ 20 words)
- Entity preservation verification
- Domain register matching

## Before / After

**Before:**
> I recently spent five unforgettable days in Lisbon, and let me tell you — this city completely stole my heart. Nestled along the banks of the Tagus River, Lisbon stands as a vibrant testament to Portugal's enduring spirit.

**After:**
> I spent five days in Lisbon last October and still have mixed feelings about it. Beautiful, yes. Also harder on the knees than anyone warned me. The hills are the whole story and somehow never make the brochures.

## File Structure

```
HumaniserUltra/
├── SKILL.md              # The skill (401 lines)
├── README.md             # This file
├── AGENTS.md             # Quick reference for agents
├── LICENSE               # MIT
└── .claude-plugin/
    └── plugin.json       # Claude Code marketplace manifest
```

---

## Limitations

**Why detectors still flag humanized text:**

1. **RLHF fingerprints** — The "helpful assistant" register is baked into instruction-tuned models during fine-tuning. Every word an LLM generates carries this signature. The skill strips surface patterns, but the underlying probability distributions remain.

2. **Token probability clusters** — LLMs pick statistically likely next-words. Detectors measure how "surprised" they are by each word choice. Even after humanization, the text clusters where a language model would predict.

3. **Semantic collapse** — LLM text converges toward a narrower semantic space than human writing. Pattern elimination doesn't fix this — it moves text within the same collapsed distribution.

4. **Logical structure persistence** — The argumentative skeleton (how claims connect, what gets emphasis) survives surface-level rewriting. Detectors like RACE (ACL 2026) model this directly.

5. **Ensemble detection** — Modern detectors combine 5-7 signals simultaneously. Fixing one signal (vocabulary) while leaving others (burstiness, entropy, discourse) doesn't fool the ensemble.

**When it works best:** Casual content, short text, non-English, mixed human/AI text.

**When it doesn't work alone:** Academic submissions, high-stakes published content, long documents against ensemble detectors.

**For maximum evasion:** Use base model rewriting, OOD shifting, or detector feedback loops — all documented in the skill.

**Other limits:**
- No method is permanent — detectors improve continuously
- Semantic preservation and detection evasion are in tension
- Rule-based rewriting cannot fully remove RLHF fingerprints from instruction-tuned output

## License

MIT
