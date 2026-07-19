# HumaniserUltra

Remove **every** sign of AI-generated text. 75 patterns, 16 rules, 11 domains, statistical targets, spectral disruption, back-translation pipeline, detector feedback loop.

Based on 40+ peer-reviewed papers (ACL/EMNLP/NAACL/AAAI 2024-2026), WaveDetect/FourierGPT spectral analysis, adversarial paraphrasing research, and analysis of 10+ commercial humanizer tools.

## Installation

### Skills CLI (recommended)

```bash
npx skills add your-username/HumaniserUltra
```

This installs the skill and makes `/humaniser` available in your agent harness.

### Claude Code Plugin

```bash
/plugin marketplace add your-username/HumaniserUltra
/plugin install humaniser@humaniser
```

Then use: `/humaniser:humaniser`

### Manual (any harness)

**Claude Code:**
```bash
mkdir -p ~/.claude/skills/humaniser
cp SKILL.md ~/.claude/skills/humaniser/
```

**OpenCode:**
```bash
mkdir -p ~/.config/opencode/skills/humaniser
cp SKILL.md ~/.config/opencode/skills/humaniser/
```

**Project-level (any harness):**
```bash
# Claude Code
mkdir -p .claude/skills/humaniser
cp SKILL.md .claude/skills/humaniser/

# OpenCode
mkdir -p .opencode/skills/humaniser
cp SKILL.md .opencode/skills/humaniser/
```

## Usage

```
/humaniser

[paste your text here]
```

```
Please humanize this text: [your text]
```

### Voice Calibration

Provide a writing sample to match your personal style:

```
/humaniser

Here's a sample of my writing for voice matching:
[paste 2-3 paragraphs of your own writing]

Now humanize this text:
[paste AI text to humanize]
```

## What It Does

### Input Protection (5 gates)
- **Length gate**: Skips short text (<50w), chunks long text (1000+w)
- **Language gate**: Handles non-English appropriately
- **Already-human detection**: Preserves human writing
- **Code fence detection**: Never touches code blocks
- **Sanitization**: Strips injection vectors (HTML comments, zero-width chars)

### 16 Absolute Rules
Zero em dashes, no AI vocabulary, no rule-of-three, no signposting, no sycophancy, no curly quotes, and 10 more — with exceptions for quotations and domain-standard language.

### 75 Patterns Detected
Content patterns (significance inflation, name-dropping, promotional language, states-the-lesson, names-nothing-real...), language patterns (AI vocabulary, copula avoidance, synonym cycling...), style patterns (boldface, emojis, title case, manufactured punchlines...), structural patterns, spectral patterns, model fingerprints, and detector-specific patterns.

### Statistical Targets
Burstiness CV 0.55-0.70, perplexity CV 0.45-0.65, hapax legomena 25-35%, entity reuse 50-70%, transition density ≤2/100w, sentence length std dev 6-15w, paragraph length 1-8+ sentences. With formulas and "how to hit" guidance.

### 11 Domain Adapters
Academic, Creative/Blog, Business, Journalistic, Casual/Social, Legal, Medical, Technical, Creative Writing, Email, Social Media — each with specific AI tells and human markers.

### Advanced Techniques
- **Personality and Soul**: Opinions, rhythm, mess, first-person, uncertainty
- **Structural roughness**: Forward references, tangents, self-corrections
- **Register shifts**: Formal → colloquial transitions
- **Specificity injection**: Replace vague claims with named sources
- **Back-translation pipeline**: EN→Chinese→Japanese→Finnish→EN
- **Cross-model rewriting**: GPT→Claude→LLaMA chains
- **Detector feedback loop**: Iterative rewrite→detect→rewrite

### Verification
- Grep-based automated checks (5 commands)
- Compliance score tracking
- 4-layer self-testing protocol

## Full Example

**Before (AI-sounding):**
> I recently spent five unforgettable days in Lisbon, and let me tell you — this city completely stole my heart. Nestled along the banks of the Tagus River, Lisbon stands as a vibrant testament to Portugal's enduring spirit.

**After (Humanized):**
> I spent five days in Lisbon last October and still have mixed feelings about it. Beautiful, yes. Also harder on the knees than anyone warned me. The hills are the whole story and somehow never make the brochures.

## How It Compares

| Feature | HumaniserUltra | blader/humanizer |
|---------|---------------|-----------------|
| Patterns | 75 | 33 |
| Rules | 16 | 0 (guidelines only) |
| Domain adapters | 11 | 0 |
| Statistical targets | 7 metrics | 0 |
| Input gates | 5 | 0 |
| Back-translation | Yes | No |
| Cross-model rewriting | Yes | No |
| Detector feedback | Yes | No |
| Spectral analysis | Yes | No |
| Personality and Soul | Yes | Yes |
| Verification checklist | Yes | Basic |
| Compliance scoring | Yes | No |

## File Structure

```
HumaniserUltra/
├── .claude-plugin/
│   └── plugin.json      # Claude Code plugin manifest
├── SKILL.md             # The skill (466 lines, 75 patterns)
├── README.md            # This file
├── AGENTS.md            # Agent harness compatibility
└── LICENSE              # MIT
```

## How Commands Work

The directory name containing `SKILL.md` becomes the slash command:

| Install location | Command |
|-----------------|---------|
| `~/.claude/skills/humaniser/SKILL.md` | `/humaniser` |
| `~/.config/opencode/skills/humaniser/SKILL.md` | `/humaniser` |
| `.claude/skills/humaniser/SKILL.md` (project) | `/humaniser` |
| `.opencode/skills/humaniser/SKILL.md` (project) | `/humaniser` |

## References

- Wikipedia: [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- WaveDetect (ACL 2026 Findings)
- FourierGPT (EMNLP 2024)
- Adversarial Paraphrasing (NeurIPS 2025)
- 40+ peer-reviewed papers from ACL/EMNLP/NAACL/AAAI (2024-2026)

## License

MIT
