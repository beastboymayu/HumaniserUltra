# HumaniserUltra

Professional editing tool that transforms stiff, formulaic text into natural, engaging writing.

## Install

One command, works everywhere:

```bash
npx skills add beastboymayu/HumaniserUltra
```

Or per harness:

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

Manual install:

```bash
# Any harness
mkdir -p .agents/skills/humaniser && cp SKILL.md .agents/skills/humaniser/

# Claude Code
mkdir -p ~/.claude/skills/humaniser && cp SKILL.md ~/.claude/skills/humaniser/

# OpenCode
mkdir -p ~/.config/opencode/skills/humaniser && cp SKILL.md ~/.config/opencode/skills/humaniser/
```

## Usage

```
/humaniser
[paste AI text to humanize]
```

Write from scratch:

```
/humaniser
Write me an email asking for a raise
```

Match your voice:

```
/humaniser
Here's how I write: [paste your writing sample]
Now write this in my voice: [topic]
```

## What It Does

Strips the obvious stuff first. Zero em dashes. 47 banned words (delve, tapestry, pivotal, robust). No "Let's dive in." No "Great question!" No rule-of-three forcing.

Then it adds what AI text is missing. Personality. Opinions. Specific details instead of "research shows." Register shifts mid-paragraph. Tangents and self-corrections. The messy parts that make writing feel like a person wrote it.

Covers 12 domains: Academic, Creative, Business, Journalistic, Casual/Social, Legal, Medical, Technical, Creative Writing, Grant Proposals, Resumes/CVs, Multi-Domain. Each has its own rules. Legal preserves terms of art. Academic keeps passive voice in Methods. Medical keeps "Furthermore" because that's how clinicians actually write.

Handles the tricky stuff too. Six input gates catch short text, non-English, already-human writing, code blocks, tables, and injection vectors. Voice calibration matches your writing style from a sample. Long documents get chunked with a voice bible so paragraph 40 sounds like paragraph 1.

For high-stakes content, it escalates. Base model rewriting (detectors fire on RLHF artifacts, not AI-ness). OOD shifting (push text out of the detector's training distribution, 50x better than pattern elimination). Detector feedback loops. Back-translation through Chinese, Japanese, and Finnish.

Every output gets a compliance score. Em dashes, banned words, signposting, burstiness, entity preservation, domain matching. If anything fails, it fixes before returning.

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

---

## Limitations

Every language model leaves statistical traces in its output. Rules remove surface patterns, but underlying probability distributions remain.

LLMs pick statistically likely next-words. Even after editing, the text may cluster where a language model would predict.

LLM text converges toward a narrower semantic space than human writing. Surface editing doesn't fully fix this.

The argumentative skeleton survives surface-level editing. How claims connect, what gets emphasis.

Modern analysis tools combine multiple signals simultaneously. Fixing one signal while leaving others doesn't fool the ensemble.

**Works best on:** Casual content, short text, mixed human/machine text.

**Doesn't work alone on:** Academic submissions, high-stakes published content, long documents.

**For maximum quality:** Cross-model rewriting, register shifting, or iterative quality feedback. All documented in the skill.

Other limits: no method is permanent, semantic preservation and style variety are in tension, and surface editing cannot fully remove model-specific patterns.

## License

MIT
