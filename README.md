# HumaniserUltra

A friendly writing assistant that helps your text sound more like you wrote it.

Ever read something and thought "this feels like a robot wrote it"? That's what this skill fixes. It catches the patterns that make writing feel stiff and formulaic, then helps you add the voice, personality, and specificity that make it sound human.

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
[paste your text]
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

It catches the patterns that make writing feel stiff. No em dashes everywhere. No "delve" or "tapestry" or "robust." No "Let's dive in" or "Great question!" No rule-of-three forcing. No hedged assertions.

Then it adds what stiff writing is missing. Personality. Opinions. Specific details instead of "research shows." Register shifts mid-paragraph. Tangents and self-corrections. The messy parts that make writing feel like a person wrote it.

Covers 12 domains: Academic, Creative, Business, Journalistic, Casual/Social, Legal, Medical, Technical, Creative Writing, Grant Proposals, Resumes/CVs, Multi-Domain. Each has its own rules. Legal preserves terms of art. Academic keeps passive voice in Methods. Medical keeps "Furthermore" because that's how clinicians actually write.

Handles the tricky stuff too. Six input gates catch short text, non-English, already-human writing, code blocks, tables, and injection vectors. Voice calibration matches your writing style from a sample. Long documents get chunked with a voice bible so paragraph 40 sounds like paragraph 1.

Every output gets checked: em dashes, banned words, signposting, burstiness, entity preservation, domain matching. If anything fails, it fixes before returning.

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

## What It's Good At

Casual content, short text, mixed human/AI text, emails, blog posts, social media, creative writing. Anywhere you want writing that sounds like a person wrote it.

## What It Can't Do Alone

Academic submissions, high-stakes published content, long documents against multiple analysis tools. For those, it has advanced techniques documented in the skill (cross-model rewriting, register shifting, quality feedback loops).

## License

MIT
