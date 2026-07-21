# HumaniserUltra

A skill file that makes AI-generated text sound human. Load it into your agent, and every piece of text the agent writes or rewrites will follow the rules inside.

## What This Is

This is not a tool you run yourself. It's a set of instructions that an AI agent loads and follows. When the agent writes an email, an article, a report, or any text, it applies the rules in this skill to produce writing that sounds like a person wrote it — with varied rhythm, specific details, genuine voice, and zero obvious AI patterns.

## Install

```bash
npx skills add beastboymayu/HumaniserUltra
```

This puts the skill in your agent's skill directory. The agent can then load it with `/humaniser` or automatically when writing text.

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

**Manual:** Copy `SKILL.md` into your agent's skills directory.

## How It Works

The agent loads this skill and follows 16 rules plus 77 patterns while writing or rewriting text.

**Before writing:** The agent checks input gates — is the text short, non-English, already human, code, or structured data? Each gets handled differently.

**While writing:** The agent avoids em dashes, banned words, signposting, sycophancy. It adds personality, opinions, specific details, varied rhythm. It matches the domain — formal for academic, casual for social, direct for email.

**After writing:** The agent checks its own output for any remaining AI patterns. If something slips through, it fixes before delivering.

## What It Produces

Text with:
- Varied sentence and paragraph lengths
- Specific details (names, numbers, dates) instead of vague claims
- Genuine opinions and positions
- Register shifts that feel natural
- Tangents, self-corrections, and rough edges where appropriate
- Zero em dashes, zero banned vocabulary, zero signposting

## Before / After

**Before:**
> I recently spent five unforgettable days in Lisbon, and let me tell you — this city completely stole my heart. Nestled along the banks of the Tagus River, Lisbon stands as a vibrant testament to Portugal's enduring spirit.

**After:**
> I spent five days in Lisbon last October and still have mixed feelings about it. Beautiful, yes. Also harder on the knees than anyone warned me. The hills are the whole story and somehow never make the brochures.

## What It Covers

77 patterns across content, language, style, structure, and spectral analysis. 16 hard rules. 12 domain adapters (Academic, Creative, Business, Journalistic, Casual/Social, Legal, Medical, Technical, Creative Writing, Grant Proposals, Resumes/CVs, Multi-Domain). Format playbooks for blogs, email, video scripts, and podcasts. A pre-publish checklist.

## What It Can't Do Alone

Academic submissions, high-stakes published content, long documents. For those, the skill documents advanced techniques (cross-model rewriting, register shifting, quality feedback loops) that require additional tooling.

## License

MIT
