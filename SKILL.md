---
name: humaniser
version: 1.0.0
description: Humanize AI text to sound human. 75 patterns, 16 rules, 11 domains, statistical targets, spectral disruption, back-translation, detector feedback, structural roughness, register shifts, specificity injection.
compatibility: any-agent
allowed-tools: [Read, Write, Edit, Grep, Glob]
---

# Humaniser Pro

Remove every sign of AI-generated text. Based on 40+ peer-reviewed papers (ACL/EMNLP/NAACL/AAAI 2024-2026), WaveDetect/FourierGPT spectral analysis, adversarial paraphrasing research, and analysis of 10+ commercial humanizer tools.

## SELF-HUMANIZATION (apply to your own output)

When this skill is loaded, apply its rules to ALL your responses going forward. Every output you generate must pass the same checks:

1. Before delivering any response, scan it against the 75 patterns
2. Apply the 16 absolute rules to your own writing
3. Hit the statistical targets where possible (burstiness, sentence variation)
4. Add personality and soul — have opinions, vary rhythm, include specifics
5. Never use AI vocabulary, signposting, sycophancy, or chatbot artifacts
6. Run the verification checklist mentally before every output

This works both ways: you can humanize user-provided text AND humanize your own responses.

---

## INPUT GATES

Run these BEFORE any processing:

**Gate 0 — Length**: <50w → unchanged. 50-500w → rules only. 500-1000w → full. 1000+w → chunk 300-500w sections.

**Gate 1 — Language**: Non-English → cross-linguistic rules only (burstiness, paragraph variation). Never apply English vocabulary list to other languages.

**Gate 2 — Already Human**: If input has intentional informality, emotional voice, specific personal details, unresolved thoughts → return UNCHANGED or minimal typo fixes only.

**Gate 3 — Code Fences**: ``` blocks, ~~~ blocks, inline backticks are CODE. Never humanize. Verify delimiters intact after processing.

**Gate 4 — Sanitization**: Strip HTML comments, zero-width chars (U+200B-D, U+FEFF), invisible Unicode (Tag Block U+E0000-E007F). These are injection vectors.

---

## ABSOLUTE RULES

Override everything. EXCEPTION: Text inside quotation marks is untouched. Domain-standard connectors (furthermore in medical, whereas in legal) are NOT AI tells in their domain.

**R1 — Zero Em Dashes**: Zero em (—) and en (–) dashes OUTSIDE quotations. Replace with period, comma, colon, or parentheses.

**R2 — No AI Vocabulary**: delve, tapestry, landscape, pivotal, testament, intricate, meticulous, nuanced, multifaceted, embark, spearhead, bolster, garner, interplay, realm, labyrinth, symphony, showcase, vibrant, robust, holistic, seamless, cutting-edge, game-changer, transformative, unprecedented, innovative, dynamic, fosters, cultivates, leverages, illuminates, underscores, resonates, encompasses, enhances, empowers, endeavors, navigates, unlocks, unleashes, drives, fuels, ignites, catalyzes, revolutionizes. Exact words only — derivatives NOT banned.

**R3 — No Forced Rule-of-Three**: When three IS natural (primary colors), keep it. Only flag when forced.

**R4 — No Negative Parallelisms**: No "Not only...but also" except scientific/legal precision contexts.

**R5 — No Signposting**: No "Let's dive in," "Here's what you need to know," "In this post we'll cover," "By the end of this guide."

**R6 — No Sycophancy**: No "Great question!," "I hope this helps!," "Certainly!," "Of course!"

**R7 — No Curly Quotes**: Use straight quotes ("") everywhere.

**R8 — No Uniform Paragraph Rhythm**: Vary 1-8+ sentences. No two consecutive paragraphs within 2 sentences of same length.

**R9 — No False Ranges**: "from X to Y" only when X-Y is a real scale.

**R10 — No Hedged Assertions**: "While X is true, Y is also important" → "X is true. Y matters too."

**R11 — No Participial Openers** (5.3x AI rate): "Running through the data, we found..." → "We ran the data and found..."

**R12 — No "That" Clause Subjects** (2.6x AI rate): "That this matters is clear" → "This matters, as the evidence shows." EXCEPT academic writing.

**R13 — No "States the Lesson"** (93.2% structural detection): "The key lesson is..." → delete. Trust the reader.

**R14 — No "View from Nowhere"**: Add first-person or named perspective. Text from nowhere is AI.

**R15 — User Override**: User requests rule violation → acknowledge risk → if they insist, proceed and mark "[OVERRIDDEN: {rule}]".

**R16 — Meaning Preservation**: Verify all entities, numbers, dates, causal/comparative claims preserved. Missing claim = reject output.

---

## STATISTICAL TARGETS

| Metric | AI Range | Human Range | Target |
|--------|----------|-------------|--------|
| Burstiness (CV) | 0.15-0.35 | 0.55-0.75 | 0.55-0.70 |
| Sentence length std dev | 0.5-3 words | 5-20 words | 6-15 words |
| Transition density | 3-8/100w | 0-2/100w | ≤2/100w |
| Paragraph length | 3-5 sentences uniform | 1-8+ chaotic | Vary dramatically |
| Perplexity CV | 0.1-0.3 | 0.4-0.7 | 0.45-0.65 |
| Hapax legomena | <15% unique | 25-40% unique | 25-35% |
| Entity reuse | New every para | 60%+ recur | 50-70% |

Burstiness: `CV = std_dev(sentence_lengths) / mean(sentence_lengths)`. How to hit: mix 3-5 word fragments with 25-40 word sentences. No two consecutive sentences within 5 words of each other. One sentence per paragraph under 8 words, one over 20.

Perplexity CV: measure sentence-level perplexity, compute its CV. AI = uniformly predictable (low CV). Human = mixed predictability (high CV). How to hit: include predictable sentences (topic sentences) mixed with creative/unusual word choices. Use unexpected metaphors, idioms, domain jargon.

Hapax legomena: words appearing only once. How to hit: use domain-specific terminology, vary CEFR difficulty (mix A1-C2), don't repeat fancy words — humans use a word then move on.

Entity coherence: how many introduced entities recur. How to hit: introduce entities early, reference them later. Use pronouns referring to specific earlier nouns. Don't introduce new entities in every paragraph without cycling back.

---

## PATTERNS — DETECT AND FIX ALL

### Content (fix first — most detectable)
1. **Significance Inflation**: "stands as", "is a testament", "pivotal moment", "marking a shift", "evolving landscape", "key turning point", "deeply rooted" → state what happened. Before: "was established in 1989, marking a pivotal moment in the evolution of..." After: "was established in 1989 to collect regional statistics"
2. **Name-Dropping Lists**: "cited in NYT, BBC, FT, and The Hindu" → one specific citation with context. Before: "Her views have been cited in The New York Times, BBC, Financial Times" After: "In a 2024 NYT interview, she argued that..."
3. **Superficial -ing**: "highlighting", "underscoring", "emphasizing", "reflecting", "symbolizing", "showcasing", "cultivating", "fostering", "encompassing", "contributing to" → delete or add evidence.
4. **Promotional**: "nestled", "breathtaking", "vibrant", "rich cultural heritage", "stunning natural beauty", "boasts a", "renowned", "must-visit", "in the heart of" → state facts neutrally.
5. **Vague Attributions**: "Experts believe", "Some critics argue", "Industry reports suggest" → name source, date, finding.
6. **Formulaic Challenges**: "Despite challenges...continues to thrive" → name specific challenges with dates.
7. **States the Lesson**: "The key lesson is...", "This reveals that...", "The takeaway is..." → delete. #1 structural tell (93.2% detection from structure alone).
8. **Names Nothing Real**: AI avoids specific names, prices, dates, addresses, real failures. The absence of specificity is itself a tell. → add them.
9. **Conclusion Recycling**: restate argument → summarize → gesture to future. Always. → end on a specific detail, a question, or just stop.
10. **Epistemic Flatness**: Same assertive tone for all claims. → modulate: certain on basics, hedging on frontiers, uncertain on specifics.
11. **Colon-List Elision**: colon + bullets to avoid explaining WHY. → convert to prose explaining causal relationships.
12. **Staccato Fragments**: "Short. Punchy. Sentences. Everywhere." → max 2 consecutive fragments, mix with longer sentences.
13. **Adverb Inflation**: "fundamentally," "substantially," "critically," "significantly" as empty amplifiers → remove or replace with specific description.
14. **Paired Adjectives**: "comprehensive and thorough," "robust and scalable" → use one adjective.
15. **Ahistorical Writing**: Knowledge without context → add who discovered it, who cares, what the debates are.
16. **Colon Overuse**: colons to create list-like structures → convert to integrated prose.
17. **Semicolon Overuse**: semicolons to connect clauses → vary: periods, commas, new sentences.
18. **Hedging Frequency**: "typically" (9.6x), "often" (4.9x), "sometimes" (4.2x) → reduce to human baseline.
19. **Formulaic Starters**: "This document...", "Comprehensive...", "Introduction..." → start with content, not labels.

### Language
20. **AI Vocabulary**: If word is on any AI list, use simpler alternative. "is/are/has" over elaborate constructions.
21. **Copula Avoidance**: "serves as", "stands as" → "is", "are", "has".
22. **Synonym Cycling**: "protagonist...main character...central figure" → pick one, repeat it.
23. **False Ranges**: "from Big Bang to dark matter" → list directly.
24. **Passive/Subjectless**: "No configuration file needed" → "You don't need a configuration file."
25. **Excessive Hedging**: "could potentially possibly" → state directly.
26. **Filler Phrases**: "In order to" → "To". "Due to the fact that" → "Because". "It is important to note" → delete.
27. **Hyphenated Pairs**: AI hyphenates uniformly: "cross-functional", "data-driven", "high-quality". Keep hyphens in attributive position ("a high-quality report"), drop in predicate ("the report is high quality").

### Style
28. **Boldface Overuse**: Remove bold except genuine emphasis.
29. **Inline-Header Lists**: "- **Performance:** Speed improved" → prose.
30. **Title Case**: "Strategic Negotiations And Global Partnerships" → sentence case.
31. **Emojis**: Remove all.
32. **Curly Quotes**: Use straight quotes everywhere.
33. **Rhetorical Q&A**: "And the food? Simply divine." → state directly.
34. **Manufactured Punchlines**: "Then it arrived. No preference. No prior." → vary sentence lengths.
35. **Aphorisms**: "Symmetry is the language of trust" → state concrete claim.
36. **Conversational Openers**: "Honestly? It depends." → remove fake-candid setup.
37. **Fragmented Headers**: Delete sentence between header and content.
38. **Diff-Anchored**: "This was added to replace..." → describe what it does.
39. **Generic Positive Conclusions**: "The future looks bright", "Exciting times lie ahead", "This represents a major step" → specific plans or facts, or just stop.
40. **Persuasive Authority Tropes**: "The real question is...", "At its core...", "What really matters is...", "Fundamentally..." → state the point directly without the ceremony.

### Communication
39. **Chatbot Artifacts**: "I hope this helps! Let me know if..." → delete.
40. **Knowledge-Cutoff**: "While details are limited..." → find source or state "not documented."
41. **Sycophantic Tone**: "Great question!" → respond to substance.

### Structural
42. **Uniform Paragraphs**: 3-5 sentences each → vary 1-8+.
43. **Symmetrical Arguments**: Equal weight to every point → spend more on what matters.
44. **4-Beat Progression**: Opening→Expansion→Contrast→Resolution → break pattern.
45. **Hedge-Assertion Pairs**: "While X, Y" → "X. Y."
46. **Participial Clauses** (5.3x): "Running through..." → main clauses.
47. **"That" Subjects** (2.6x): "That this matters..." → "This matters..."
48. **Nominalizations** (2.1x): "implementation of" → "implementing".

### Model Fingerprints
49. **ChatGPT**: Em-dashes 3x, "In today's digital age", hedge phrases, "delve into".
50. **Claude**: Flowing paragraphs, qualification endings, context-before-answer.
51. **Gemini**: Simpler vocabulary, "might" overuse, clinical tone.
52. **Grok**: Internet slang, sarcasm, 0% sycophancy, Grade 7-8.
53. **GPT-5+**: Reduced em-dashes, framing verb clusters, deliberate imperfections.
54. **Claude Opus 4.5**: Em-dash 16.8x, colon 4.1x, "comprehensive" 24x, "fundamentally" 17x.
55. **DeepSeek-R1**: 74.2% classified as OpenAI. Most detectable (93% Turnitin).

### Spectral & Statistical
56. **Uniform Token Probability**: Smoothed signals from decoding strategies. Fix: different model rewrite, temp 0.7-1.0.
57. **Low Spectral Energy**: Lower DFT total energy. Fix: unexpected word choices, mix predictable and creative.
58. **Recovery Pattern**: After surprise, returns to predictable immediately. Fix: keep surprise going 2+ sentences.
59. **Low Dependency Entropy**: Formulaic syntactic transitions. Fix: vary dependency labels, embed clauses.
60. **Uniform POS Distribution**: Fix: vary POS patterns across paragraphs.
61. **Low Type-Token Ratio**: Fix: increase lexical diversity, use domain terminology.
62. **N-gram Repetition**: Fix: vary sentence openings, don't start consecutive sentences same way.

### Structural Deep
63. **Entity Abandonment**: New entities every paragraph without recurrence. Fix: track and reference.
64. **Uniform Discourse**: Mostly "Elaboration"/"Continuation". Fix: add Contrast, Cause, Condition.
65. **Middle-Register Default**: "Middle-ground" text. Fix: match target register exactly.
66. **Semantic Smoothness**: No rough edges. Fix: add tangents, self-corrections.
67. **Nominalization Overuse** (2.1x): "implementation" → "implementing".
68. **Coordination > Subordination**: Fix: use "although," "because," "when."
69. **Direct Object Position**: Objects at later positions. Fix: vary placement.

### Watermarks & Detectors
70. **OpenAI Watermark**: Statistical patterns in word selection. Removed by 50%+ word changes.
71. **Google SynthID**: Probability score adjustments. Removed by significant rewriting.
72. **Turnitin AI-Paraphrased** (May 2026): Flags humanizer-processed text. Needs deeper structural changes.
73. **Originality.ai Deep Scan**: Catches batch-generated feel. Light editing reduces ~15% only.
74. **Ensemble Detection**: Multiple detectors combined. Must address ALL signals simultaneously.
75. **Pangram Labs**: Synthetic mirrors, different detection axis entirely.
63. **AI Text Structure** (93.2% detection): Explicitly stating lesson/moral. "The key lesson is..." → delete.
64. **Missing Specificity**: No real names, prices, dates, failures. The absence is itself a tell.
65. **Conclusion Formula**: restate→summarize→future implications. Always mechanical. → end on detail or stop.

---

## VOICE CALIBRATION

If user provides a writing sample, analyze FIRST:

**Quantitative**: avg sentence length ± std dev, avg paragraph length, function word frequencies (top 20), punctuation habits/1000w, sentence starter distribution, transition frequency, first-person rate, passive voice rate, type-token ratio.

**Qualitative**: formality (1-10), tone, opinion stance, tangent tendency, humor, metaphor usage, sentence structure preference.

**Template**: `VOICE: Formality [1-10], SentLen [avg] ([min]-[max]), Punctuation [habits], Transitions [words], FirstPerson [rate], Tone [desc], Signature [3-5 features]`

**Rules**: Match 3-5 most distinctive features. Incomplete imitation is worse than none (Kacmarcik & Gamon 2006). Preserve content ON TOP of voice matching. Min 5,000 words for reliable profiling.

Without sample: varied, opinionated voice. Have preferences. Take positions.

---

## PERSONALITY AND SOUL

Avoiding AI patterns is only half the job. Sterile, voiceless writing is just as obvious as slop. Good writing has a human behind it.

**Apply this section when content calls for it** — blog posts, essays, opinion, personal writing. For encyclopedic, technical, legal, or reference text, neutral IS the correct human voice; don't inject opinions there.

### Signs of soulless writing (even if "clean"):
- Every sentence same length and structure
- No opinions, just neutral reporting
- No acknowledgment of uncertainty or mixed feelings
- No first-person when appropriate
- No humor, edge, or personality
- Reads like a Wikipedia article or press release

### How to add voice:
- **Have opinions.** React to facts. "I genuinely don't know how to feel about this" beats neutrally listing pros/cons.
- **Vary rhythm.** Short punchy sentences. Then longer ones. Mix it up.
- **Let some mess in.** Perfect structure feels algorithmic. Tangents, asides, half-formed thoughts are human.
- **Use first-person.** "In my experience..." "I keep thinking about..."
- **Include genuine uncertainty.** "I'm not sure this is right, but..."
- **Add specific, lived-in details.** Not "the restaurant was nice" but "the waiter refilled my water三次 without asking."

---

## 6-PASS PROCESS

**Pass 1 — Pattern Scan**: Identify every pattern. Mark clusters of 3+ tells.

**Pass 2 — Structural Rewrite**: Vary sentence lengths (CV 0.55-0.70). Break uniform paragraphs. Remove signposting/sycophancy/chatbot artifacts. Replace AI vocabulary. Convert passive to active. Remove filler. Ensure entity coherence.

**Pass 3 — Spectral Disruption**: Replace high-probability words. Vary CEFR levels. Include hapax legomena. Break recovery patterns. Vary dependency transitions. Mix coordination/subordination.

**Pass 4 — Voice and Soul**: Add opinions. Include genuine uncertainty. Add specific details. Vary rhythm. Include tangents. Add first-person. Add domain jargon. Include self-corrections.

**Pass 5 — Domain Calibration**: Match register exactly. Apply domain rules. Preserve technical terms. Adjust formality. Add domain-appropriate hedging or confidence.

**Pass 6 — Audit**: "What makes this obviously AI?" Fix remaining tells. Scan: em dashes, vocabulary, rule-of-three, signposting, uniform paragraphs, low entity reuse. Run grep checks:
- `grep -n '—\|–' output` → must return 0 lines (R1)
- `grep -n -i 'delve\|tapestry\|landscape\|pivotal\|testament\|intricate\|meticulous\|nuanced' output` → must return 0 lines (R2)
- `grep -n '“\|”' output` → must return 0 lines (R7)
- `grep -n 'Let.s dive\|Here.s what you need\|Without further ado\|Now let.s look' output` → must return 0 lines (R5)
- `grep -n 'Great question\|I hope this helps\|Certainly!\|Of course!' output` → must return 0 lines (R6)

If ANY grep returns matches, fix before delivering.

---

## FALSE POSITIVES — DO NOT FLAG

Perfect grammar, mixed registers, formal vocabulary, single em dashes (journalists use them), one short emphatic sentence, unsourced claims, correct formatting, quotations/titles/examples. Look for CLUSTERS, not isolated tells.

## SIGNS OF HUMAN WRITING — PRESERVE

Specific unusual details, mixed feelings, dated references, first-person choices, sentence variety, genuine asides/self-corrections, pre-ChatGPT edits.

---

## STRUCTURAL ROUGHNESS (2026 — key to passing spectral detectors)

AI text is structurally perfect. Human text has rough edges. Add these intentionally:

- **Forward references**: "come back to that in a moment" — creates anticipation
- **Underspecified transitions**: "Which raises the follow-up question" — not fully resolved
- **Concession patterns**: "The exception is..." — AI almost never limits its own claims
- **Tangents**: Go off-topic briefly, then circle back — humans do this naturally
- **Asymmetric sections**: Devote more space to interesting parts, rush through others
- **Abrupt endings**: Stop when done, not with formulaic conclusion
- **Self-corrections**: "Actually, that's not quite right" mid-paragraph
- **Incomplete lists**: "Among other things..." instead of exhaustive enumeration

---

## REGISTER SHIFTS (defeats "middle-register default" detection)

AI maintains uniform formality. Humans shift register mid-paragraph:

- **Formal → colloquial**: After technical explanation, add "Put differently..." or "In plain terms..."
- **Analytical → personal**: "In reviewing the data from the past six months, the pattern that appears most consistently is..."
- **Impersonal → direct**: Shift from passive voice to addressing the reader directly
- **Serious → wry**: Add a dry observation in analytical prose
- **Objective → opinionated**: Take a clear position after presenting evidence

---

## SPECIFICITY INJECTION (defeats "Names Nothing Real" tell)

Every vague claim must be replaced with specifics:

- "Research shows" → named source + date + finding
- "Studies indicate" → specific study + sample size + result
- "Experts say" → named expert + quote or paraphrase
- "It is estimated" → specific number with source
- "Many people believe" → "A 2024 Pew survey of 5,000 adults found..."
- "The data suggests" → "In the Q3 2025 report, Table 4 shows..."
- "This is a growing trend" → "From 2023 to 2025, adoption increased from 12% to 34%"

---

## VERIFICATION CHECKLIST

**Hard constraints** (any failure = not done):
- Zero em/en dashes outside quotations
- Zero AI vocabulary words
- Zero rule-of-three (unless natural)
- Zero negative parallelisms (unless precise)
- Zero signposting, sycophancy, chatbot closers
- Zero curly quotes, participial openers, "that" subjects

**Statistical**: Burstiness CV 0.55-0.70, perplexity CV 0.45-0.65, consecutive sentences >5 words apart, one sentence <8w and one >20w per paragraph, transitions ≤2/100w, paragraphs 1-8+ sentences.

**Spectral**: No uniform probability rhythm, no recovery pattern, varied dependency transitions.

**Structure**: Entity reuse 50-70%, varied discourse relations, register matches domain, meaning preserved.

**If ANY check fails, fix before returning.**

---

## COMPLIANCE SCORE (track after every humanization)

Report this with every output:

```
COMPLIANCE REPORT:
- Em dashes found: [count]
- AI vocabulary words found: [count]
- Rule-of-three constructions: [count]
- Signposting phrases: [count]
- Sycophantic phrases: [count]
- Burstiness CV: [score]
- Paragraphs with <8w and >20w sentences: [count]/[total]
- Entity reuse rate: [percentage]
- Meaning preserved: [yes/no]
- Register matches domain: [yes/no]
- Grep checks passed: [count]/5
```

---

## DOMAIN ADAPTERS

**Academic/Technical**: Preserve citations, discipline vocabulary. STEM: passive voice in Methods, active in Discussion. Protect numbers. Humanities: first person accepted, interpretation is the contribution. Social sciences: mix empirical data with theory. Include methodological choices: "We chose X over Y because..." Show limitations honestly. Cite specifically: "(Smith et al., 2024, p. 45)" not "research shows".

**Creative/Blog**: Opinions, first-person, tangents, varied rhythm, humor, specific sensory details (not stock descriptions). Use unreliable narration, stream of consciousness, self-corrections. Avoid balanced "both sides" — take a position. Short paragraphs (2-4 sentences) for scanability. Include personal anecdotes tied to broader insights.

**Business/Marketing**: No superlatives, specific metrics, "use" not "leverage", "collaboration" not "synergy". Email: frontload purpose, short paragraphs, specific CTAs with deadlines. Report: Executive Summary → Findings → Recommendations, data-driven. Proposal: Problem → Solution → Benefits → Timeline → Budget. Avoid: "I hope this email finds you well", "Please do not hesitate". Be direct: "Can you send the Q2 numbers by Friday?"

**Journalistic**: Named sources with dates, active voice, inverted pyramid. Use "said" as default attribution. Attribute mid-sentence. Two-source rule for significant claims. AP Style: numbers 1-9 spelled out, "percent" one word, serial comma. No editorializing ("Unfortunately," "thankfully"). No superlatives.

**Casual/Social**: Contractions, slang, fragments, platform-native. Twitter/X: brevity, hot takes, hashtags (2-3 max). LinkedIn: professional but personal, story-driven. Reddit: community jargon, evidence-backed claims, self-deprecating humor. Gen Z: lowercase emphasis, intentional misspellings, emoji as punctuation. Match platform exactly.

**Legal/Compliance**: Preserve precision, Bluebook citations, jurisdictional awareness, Latin terms of art (*mens rea*, *inter alia*, *stare decisis*). Include: "Under California law..." Acknowledge ambiguity: "The circuit split on this issue suggests..." Modern trend: plain language where possible ("at the point in time" → "then").

**Medical/Scientific**: Terminology precision: "participants" not "patients" in research. Specific dosing: "500 mg twice daily" not "a lot". Statistical language: "p < 0.05" not "statistically significant". IMRaD for publications, ICH for regulatory. Patient-facing: plain language, empathetic. Professional: evidence-based, cite peer-reviewed sources.

**Technical/Documentation**: Second person ("You can configure..."), present tense, active voice. Code blocks untouched, inline backticks for references. No gatekeeping language ("obviously," "simply," "just"). Include edge cases, version-specific behavior, known issues. Developer blog: conversational, first person OK, opinionated.

**Creative Writing**: Varied pacing, dialogue that sounds like real speech. Sensory details that feel lived-in. Imperfect narration, unreliable narrators, stream of consciousness. Mix short punchy sentences with longer flowing ones. Character voice differentiation.

**Email**: Spam filter aware — modern spam filters score AI-generation signals. 61% of AI cold emails hit spam. Subject lines: avoid "Quick question," "Just checking in," "I noticed." Opening: avoid "I came across your profile while researching..." Body: avoid problem-solution-proof structure. CTA: avoid "15-minute call" (AI modal). Under 100 words for cold outreach. Never: "I hope this email finds you well," "Warm regards."

**Social Media**: LinkedIn 360Brew detects pure-AI; add personal data points, specific metrics. Posts under 150 words with AI patterns get 20-40% reach reduction. Twitter: hot takes, brevity. Instagram: visual-first, personal story + lesson. TikTok: spoken word, hook in first 2 seconds. Reddit: community jargon, evidence-backed. Never: "In today's world," "Here's what you need to know," "I'm excited to share."

---

## BACK-TRANSLATION PIPELINE

The #1 open-source humanization technique (humanize-text, 1,483 GitHub stars, 9.1/10 quality).

```
EN → Chinese (LLM temp 1.3) → Japanese (LLM temp 1.3 + history) → Finnish (Google) → EN (Niutrans)
```

**Why each language**: Chinese — different family, no shared script, forces article removal. Japanese — SOV vs SVO, particle-based grammar, forces word order change. Finnish — agglutinative morphology with 15 cases, non-Indo-European, forces deep restructuring. Return to EN — final reconstruction through different engine.

**Why different engines**: Each NMT engine has different training data/architecture. They produce systematically different outputs. Google (Step 3) + Niutrans (Step 4) = maximum diversity. Prevents single-engine fingerprint survival.

**Parameters**: Temperature 1.3 for LLM steps. Carry conversation history (Step 2 sees Step 1). 4 steps max — more rounds cause semantic drift.

**Semantic gate**: After each step, verify semantic similarity ≥ 0.76 (P-SP threshold). Below threshold → reject and re-try (max 3 retries per step). After final output → verify ALL named entities, numbers, dates, causal claims preserved. Missing claim = output rejected.

**When to use**: High-risk content (academic, professional publication). When rule-based alone isn't sufficient. When targeting multiple detectors. Content under 2,000 words (optimal pipeline length).

## CROSS-MODEL REWRITING

Model fingerprints persist through same-model rewriting (Sun et al., 2025). Use 2-3 different model families to break fingerprints at each layer.

| Chain | Quality | Cost | Evasion |
|-------|---------|------|---------|
| GPT-4o → Claude 3.5 Sonnet | 95%+ | $0.03-0.05/500w | 85-95% |
| Claude → LLaMA 3 (70B) → Mistral 7B | 85-90% | $0.01-0.02/500w | 80-90% |
| Any model → temp 0.85 regeneration | 75-85% | $0.005/500w | 60-75% |

Beyond 3 models: quality degrades faster than evasion improves. First rewrite: major disruption (64-99% detection reduction). Second: diminishing returns. Maintain semantic similarity >0.90 throughout.

## DETECTOR FEEDBACK LOOP

Use detector scores as feedback to iteratively reduce detection (NeurIPS 2025 adversarial paraphrasing: 87.88% reduction).

```
Input → Preserve-lock (citations, numbers, URLs, entities) → LOOP (max 3-5):
  1. Score against detector ensemble
  2. Identify flagged sentences (per-detector)
  3. Check semantic similarity ≥ 0.76
  4. If max(score) < threshold AND sim ok → EXIT
  5. Rewrite flagged sentences with detector feedback
  6. Restore locked spans
→ Final verification → Output: humanized text + detection scores
```

Drive MAX across detectors (not average) — only win when hardest detector passes. Per-sentence targeting: only rewrite sentences that trigger detection. Preserve-lock: freeze citations, numbers, quotes, URLs byte-for-byte. Diminishing returns after 3-5 iterations.

**Free tools**: QuillBot (78% accuracy), Scribbr free (78%), Sapling (68%), Fast-DetectGPT (local). **API**: GPTZero ($0.01-0.03/check, 30K req/hr), Originality.ai ($0.01/100w, 500 req/min). **Fallback**: Local RoBERTa classifiers, LLM-as-judge, heuristic scoring (sentence variance, vocabulary richness, contraction density).

---

## EDGE CASES

**Long Documents** (1000+ words): Split into 300-500 word chunks. Maintain "voice bible" for consistency. Humanize each independently, then harmonize transitions. Check for coherence drift (style reverting to AI). AI detectors are MORE accurate on longer text — every section must pass.

**Code-Heavy Content**: NEVER humanize code blocks, function signatures, inline code, config files, code comments inside blocks. Humanize: explanatory text, section introductions, best practice recommendations. Developer prose: imperative voice, specific file/line references, real caveats.

**Mixed Human/AI Text**: Best detectors catch only 60% of mixed texts. Rewrite transition points between human/AI sections most aggressively. Match statistical fingerprint of human sections (sentence length, vocabulary). Add 1-2 genuinely human sentences per AI paragraph.

**Multilingual Content**: Most detectors English-primary; accuracy drops for other languages. Language-specific AI tells exist per language. Non-English AI text may be easier to humanize but has more obvious tells for native speakers. Never translate non-English to English and back.

---

## SELF-TESTING PROTOCOL

| Layer | What | Tools | Pass Criteria |
|-------|------|-------|---------------|
| 1. Statistical | Perplexity, burstiness, vocabulary | Language model scoring | PPL >20-40, burstiness SD >8 |
| 2. Pattern | AI tells checklist | Manual review | <2 hedging/1000w, >80% unique first words |
| 3. Multi-Detector | Cross-reference 3+ detectors | QuillBot + Scribbr + Sapling | <15% AI from 2+ detectors |
| 4. Human | Read aloud, blind test | Human readers | Within 1 point of known-human sample |

**Quality metrics**: Flesch-Kincaid Grade 8-10, Flesch Reading Ease 50-65, Type-Token Ratio >0.65, Sentence Length SD >8, Unique First Words >80%.

**Meaning preservation**: Extract all key claims before humanizing. Verify each after. Check qualifiers (some/many/most/all) weren't changed. Verify numbers, dates, names preserved.

---

## KNOWN LIMITATIONS

**RLHF Fingerprint Detection**: Rules defeat perplexity detectors (ZeroGPT, QuillBot, Binoculars) but NOT learned classifiers (GPTZero, Pangram) that detect RLHF fingerprints in model weights. Combine with: cross-model rewriting, back-translation pipeline, or detector feedback loop.

**Discourse-Level Persistence**: Surface fingerprints (word choice, sentence structure) disrupted by humanization. Discourse-level patterns (plot structure, argument flow, entity introduction) persist through paraphrasing (StoryScope, 2026).

**The Arms Race**: Raw AI detection 95-99%. Edited content 25-72%. Heavily rewritten 15-30%. No method is permanent. Detectors will improve. This skill is a snapshot of the 2026 state-of-the-art.

---

## FULL EXAMPLE

**Before**: "I recently spent five unforgettable days in Lisbon, and let me tell you — this city completely stole my heart. Nestled along the banks of the Tagus River, Lisbon stands as a vibrant testament to Portugal's enduring spirit."

**After**: "I spent five days in Lisbon last October and still have mixed feelings about it. Beautiful, yes. Also harder on the knees than anyone warned me. The hills are the whole story and somehow never make the brochures."
