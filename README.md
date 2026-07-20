# HumaniserUltra

Makes AI text sound human. Removes the patterns, rhythms, and vocabulary that make writing obviously machine-generated.

**Honesty first:** This skill makes text read like a human wrote it. It does NOT guarantee bypassing AI detectors. Here's why, and what to do about it.

## Why Detectors Still Flag Humanized Text

AI detectors don't just check for "delve" and em dashes. They measure deep signals that rule-based rewriting can't fully remove:

1. **RLHF fingerprints** — The "helpful assistant" register is baked into instruction-tuned models during fine-tuning. Every word an LLM generates carries this signature. The skill strips the surface patterns, but the underlying probability distributions remain.

2. **Token probability clusters** — LLMs pick statistically likely next-words. Detectors measure how "surprised" they are by each word choice. Even after humanization, the text clusters where a language model would predict.

3. **Semantic collapse** — LLM text converges toward a narrower semantic space than human writing. Pattern elimination doesn't fix this — it just moves the text within the same collapsed distribution.

4. **Logical structure persistence** — The argumentative skeleton (how claims connect, what gets emphasis) survives surface-level rewriting. Detectors like RACE (ACL 2026) model this directly.

5. **Ensemble detection** — Modern detectors combine 5-7 signals simultaneously. Fixing one signal (vocabulary) while leaving others (burstiness, entropy, discourse) doesn't fool the ensemble.

## What This Skill Actually Does

- Removes the most obvious AI tells (vocabulary, punctuation, structure) — catches 40-60% of detection signals
- Adds genuine voice, personality, and specificity — makes text engaging, not just undetectable
- Provides domain-specific guidance — doesn't break legal/medical/technical writing
- Includes escalation paths for high-stakes content (base model pipeline, OOD shifting, detector feedback)

## When It Works

- **Casual content** (blogs, emails, social posts) — detectors are less aggressive here
- **Short text** (<500 words) — detectors have less statistical signal to work with
- **Non-English text** — most detectors are English-primary, accuracy drops for other languages
- **Mixed human/AI text** — rewriting transition points and matching the human section's fingerprint

## When It Doesn't Work Alone

- **Academic submissions** — Turnitin, GPTZero, and Originality.ai are specifically trained on humanizer output
- **High-stakes published content** — ensemble detection catches surface-level changes
- **Long documents** — more text = more statistical signal for detectors

**For these cases, combine with:** base model rewriting (Section 1 of the skill), back-translation pipeline, or OOD register shifting.

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

## What's Inside

- **6 input gates** — handles short text, non-English, already-human, code blocks, tables, injection vectors
- **16 hard rules** — zero em dashes, no AI vocabulary (47 banned words), no signposting, no sycophancy
- **50 actionable patterns** (1-50) — content, language, style, structural, each with a clear fix
- **27 reference patterns** (51-77) — model fingerprints, spectral analysis, detector-specific knowledge
- **12 domain adapters** — Academic, Creative, Business, Journalistic, Casual/Social Media, Legal, Medical, Technical, Creative Writing, Grant Proposals, Resumes/CVs, Multi-Domain
- **RLHF Voice Strip** — targets what detectors actually fire on (the "helpful assistant" register)
- **Voice calibration** — extract and match a user's writing style from samples
- **Base model pipeline** — highest-leverage technique for high-stakes content
- **OOD shifting** — register changes that defeat adversarial detectors (50x better than pattern elimination)
- **Detector feedback loop** — iterative rewriting with detector scores
- **Back-translation pipeline** — EN→ZH→JA→FI→EN chain via different engines
- **Verification checklist** — mechanical checks, compliance score with every output

## Before / After

**Before:**
> I recently spent five unforgettable days in Lisbon, and let me tell you — this city completely stole my heart. Nestled along the banks of the Tagus River, Lisbon stands as a vibrant testament to Portugal's enduring spirit.

**After:**
> I spent five days in Lisbon last October and still have mixed feelings about it. Beautiful, yes. Also harder on the knees than anyone warned me. The hills are the whole story and somehow never make the brochures.

## File Structure

```
HumaniserUltra/
├── SKILL.md              # The skill (428 lines)
├── README.md             # This file
├── AGENTS.md             # Quick reference for agents
├── LICENSE               # MIT
└── .claude-plugin/
    └── plugin.json       # Claude Code marketplace manifest
```

## Known Limits

- Rule-based rewriting cannot fully remove RLHF fingerprints from instruction-tuned model output
- Ensemble detectors combining 5-7 signals are harder to defeat than single detectors
- Semantic preservation and detection evasion are in tension — maintaining meaning preserves some detection signals
- No method is permanent — detectors improve continuously

**For maximum evasion:** Use base model rewriting (Section 1), OOD shifting (Section 2), or detector feedback loops (Section 5) — all documented in the skill.

## License

MIT
