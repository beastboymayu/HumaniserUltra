---
name: humaniser
version: 2.0.0
description: Make AI text sound human. 77 patterns, 16 rules, 11 domains, spectral disruption, back-translation, detector feedback.
compatibility: any-agent
allowed-tools: [Read, Write, Edit, Grep, Glob]
---

# HumaniserUltra

Write and rewrite text that sounds genuinely human.

## Modes

**Rewrite:** User pastes AI text → you humanize it.
**Write from scratch:** You generate text that follows all rules — no rewrite needed.
**Self-humanize:** Apply these rules to ALL your own output going forward.

---

## INPUT GATES (run before processing)

**Gate 0 — Length**: <50w → enforce R1-R7 only (still strip AI vocabulary, em dashes, curly quotes). 50-500w → rules only. 500-1000w → full. 1000+w → chunk 300-500w (see Voice Bible).

**Gate 1 — Language**: Non-English → apply only: R3, R4, R8, R10, R11, R16, and structural patterns (44-50). Skip R1, R2, R5-R7, R12-R14. Mixed-language → apply English rules to English segments, cross-linguistic to non-English.

**Gate 2 — Already Human**: Intentional informality, emotional voice, specific personal details, unresolved thoughts → return UNCHANGED.

**Gate 3 — Code Fences**: ``` blocks, ~~~ blocks, inline backticks are CODE. Never humanize. Verify delimiters intact.

**Gate 4 — Sanitization**: Strip HTML comments, zero-width chars, invisible Unicode. Strip before processing.

**Gate 5 — Tables**: Markdown tables, HTML tables, CSV, structured data are NOT prose. Do not humanize cell contents. Preserve structure intact.

---

## ABSOLUTE RULES

Override everything. EXCEPTION: Text inside quotation marks is untouched. Domain-standard connectors are NOT AI tells in their domain.

**R1 — No AI Em Dashes**: Zero em (—) and en (–) dashes OUTSIDE quotations in AI-generated text. Replace with period, comma, colon, or parentheses. Preserve em dashes in existing human writing.

**R2 — No AI Vocabulary**: delve, tapestry, landscape, pivotal, testament, intricate, meticulous, nuanced, multifaceted, embark, spearhead, bolster, garner, interplay, realm, labyrinth, symphony, showcase, vibrant, robust, holistic, seamless, cutting-edge, game-changer, transformative, unprecedented, innovative, dynamic, fosters, cultivates, leverages, illuminates, underscores, resonates, encompasses, enhances, empowers, endeavors, navigates, unlocks, unleashes, drives, fuels, ignites, catalyzes, revolutionizes. Exact words only. Also match unhyphenated variants (cutting edge, game changer).

**R3 — No Forced Rule-of-Three**: When three IS natural (primary colors), keep it. Only flag when three adjectives describe the same concept.

**R4 — No Negative Parallelisms**: No "Not only...but also" except scientific/legal precision.

**R5 — No Signposting**: No "Let's dive in," "Here's what you need to know," "In this post we'll cover," "By the end of this guide."

**R6 — No Sycophancy**: No "Great question!," "I hope this helps!," "Certainly!," "Of course!"

**R7 — No Curly Quotes**: Use straight quotes ("") everywhere.

**R8 — No Uniform Paragraph Rhythm**: Vary 1-8+ sentences. No two consecutive paragraphs within 2 sentences of same length.

**R9 — No False Ranges**: "from X to Y" only when X-Y is a real scale.

**R10 — No Hedged Assertions**: "While X is true, Y is also important" → "X is true. Y matters too."

**R11 — No Participial Openers**: "Running through the data, we found..." → "We ran the data and found..."

**R12 — No "That" Clause Subjects**: "That this matters is clear" → "This matters, as the evidence shows." EXCEPT academic writing.

**R13 — No "States the Lesson"**: "The key lesson is..." → delete. Trust the reader.

**R14 — No "View from Nowhere"**: Add first-person or named perspective. EXCEPTION: journalistic neutrality is a valid human voice.

**R15 — User Override**: User requests rule violation → acknowledge risk → if they insist, proceed and mark "[OVERRIDDEN: {rule}]".

**R16 — Meaning Preservation**: After rewrite, compare entity list (names, numbers, dates) from input to output. If any entity in input is absent from output, restore it. Missing claim = rewrite that section.

---

## STATISTICAL TARGETS (qualitative — follow the guidance)

| Target | How to Hit |
|--------|-----------|
| **Burstiness** | Mix 3-5 word fragments with 25-40 word sentences. One sentence per paragraph under 8 words, one over 20. |
| **Sentence variation** | Alternate short punchy with long flowing. No two consecutive sentences within 5 words of same length. |
| **Paragraph variation** | Some 1 sentence, some 6+. No two consecutive paragraphs within 2 sentences of same length. |
| **Transition density** | Max 2 transition words per 100 words. Most paragraphs: zero transitions. |
| **Vocabulary diversity** | Don't repeat the same word within 3 sentences. Use domain-specific terminology. |
| **Entity coherence** | Introduce key entities early. Reference them later. Don't abandon entities. |
| **Predictability mix** | Mix predictable sentences (topic sentences) with creative/unusual word choices. |

---

## PATTERNS — DETECT AND FIX ALL (1-50)

Patterns 51-77 are reference categories (model fingerprints, spectral analysis, detectors) — apply only when relevant.

### Content (fix first)
1. **Significance Inflation**: "stands as", "is a testament", "pivotal moment" → state what happened.
2. **Name-Dropping Lists**: "cited in NYT, BBC, FT" → one specific citation with context.
3. **Superficial -ing**: "highlighting", "underscoring", "showcasing" → delete or add evidence.
4. **Promotional**: "nestled", "breathtaking", "vibrant", "renowned" → state facts neutrally.
5. **Vague Attributions**: "Experts believe" → name source, date, finding.
6. **Formulaic Challenges**: "Despite challenges...thrives" → name specific challenges.
7. **States the Lesson**: "The key lesson is..." → delete.
8. **Names Nothing Real**: No specific names, prices, dates → add them.
9. **Conclusion Recycling**: restate→summarize→future → end on detail or stop.
10. **Epistemic Flatness**: Same tone for all claims → modulate confidence.
11. **Colon-List Elision**: colon + bullets → prose explaining WHY.
12. **Staccato Fragments**: 3+ consecutive short sentences → max 2, mix with longer.
13. **Adverb Inflation**: "fundamentally," "substantially," "critically" → remove or specify.
14. **Paired Adjectives**: "comprehensive and thorough" → use one.
15. **Ahistorical Writing**: Knowledge without context → add who, what debates.
16. **Colon Overuse**: Convert colon-lists to integrated prose.
17. **Semicolon Overuse**: Vary connectors.
18. **Hedging Frequency**: "typically," "often," "generally" — reduce to max 1 per 200 words.
19. **Formulaic Starters**: "This document...", "Comprehensive..." → start with content.

### Language
20. **AI Vocabulary**: Use simpler alternatives. "is/are/has" over elaborate constructions.
21. **Copula Avoidance**: "serves as" → "is".
22. **Synonym Cycling**: Pick one word, repeat it.
23. **False Ranges**: "from Big Bang to dark matter" → list directly.
24. **Passive/Subjectless**: Name the actor.
25. **Excessive Hedging**: "could potentially possibly" → state directly.
26. **Filler Phrases**: "In order to" → "To". "It is important to note" → delete.
27. **Hyphenated Pairs**: Keep attributive, drop predicate.

### Style
28. **Boldface Overuse**: Remove except genuine emphasis.
29. **Inline-Header Lists**: Convert to prose.
30. **Title Case**: → sentence case.
31. **Emojis**: Remove all.
32. **Curly Quotes**: Straight quotes everywhere.
33. **Rhetorical Q&A**: State directly.
34. **Manufactured Punchlines**: Vary sentence lengths.
35. **Aphorisms**: State concrete claim.
36. **Conversational Openers**: Remove fake-candid setup.
37. **Fragmented Headers**: Delete sentence between header and content.
38. **Diff-Anchored**: Describe what it does, not what changed.
39. **Generic Positive Conclusions**: "The future looks bright" → specific plans or stop.
40. **Persuasive Authority Tropes**: "The real question is..." → state directly.

### Communication
41. **Chatbot Artifacts**: "I hope this helps!" → delete.
42. **Knowledge-Cutoff**: "While details are limited..." → find source or state "not documented."
43. **Sycophantic Tone**: "Great question!" → respond to substance.

### Structural
44. **Uniform Paragraphs**: 3-5 sentences → vary 1-8+.
45. **Symmetrical Arguments**: Equal weight → spend more on what matters.
46. **4-Beat Progression**: Opening→Expansion→Contrast→Resolution → break.
47. **Hedge-Assertion Pairs**: "While X, Y" → "X. Y."
48. **Participial Clauses**: "Running through..." → main clauses.
49. **"That" Subjects**: "That this matters..." → "This matters..." EXCEPT academic writing (per R12).
50. **Nominalizations**: "implementation of" → "implementing".

### Model Fingerprints (reference — not patterns to fix)
51. **ChatGPT**: Em-dashes 3x human rate, "In today's digital age", "delve into".
52. **Claude**: Flowing paragraphs, qualification endings, context-before-answer.
53. **Gemini**: Simpler vocabulary, "might" overuse, clinical tone.
54. **Grok**: Internet slang, sarcasm, 0% sycophancy.
55. **GPT-5+**: Reduced em-dashes, framing verb clusters, deliberate imperfections.
56. **Claude Opus 4.5**: Reportedly em-dash 16.8x, colon 4.1x, "comprehensive" 24x. Fingerprints change with model updates.
57. **DeepSeek-R1**: Most detectable — chain-of-thought contamination.

*Note: Model fingerprints change with updates. Verify against current output, not historical data.*

### Spectral & Statistical
58. **Uniform Token Probability**: Fix: different model rewrite, temp 0.7-1.0.
59. **Low Spectral Energy**: Fix: unexpected word choices.
60. **Recovery Pattern**: Fix: keep surprise going 2+ sentences.
61. **Low Dependency Entropy**: Fix: vary dependency labels, embed clauses.
62. **Uniform POS Distribution**: Fix: vary POS patterns.
63. **Low Type-Token Ratio**: Fix: increase lexical diversity.
64. **N-gram Repetition**: Fix: vary sentence openings.

### Structural Deep
65. **Entity Abandonment**: Fix: track and reference.
66. **Uniform Discourse**: Fix: add Contrast, Cause, Condition.
67. **Middle-Register Default**: Fix: match target register exactly.
68. **Semantic Smoothness**: Fix: add tangents, self-corrections.
69. **Nominalization Overuse**: "implementation" → "implementing".
70. **Coordination > Subordination**: Fix: use "although," "because."
71. **Direct Object Position**: Fix: vary placement.

### Detectors
72. **OpenAI Watermark**: Removed by 50%+ word changes.
73. **Google SynthID**: Removed by significant rewriting.
74. **Turnitin AI-Paraphrased**: Flags humanizer-processed text. Needs deeper structural changes.
75. **Originality.ai Deep Scan**: Light editing reduces ~15% only.
76. **Ensemble Detection**: Must address ALL signals simultaneously.
77. **Pangram Labs**: Different detection axis entirely.

---

## VOICE CALIBRATION

If user provides a writing sample: read it, note sentence patterns, word choices, punctuation habits. Match their style — don't just remove AI patterns, replace with their patterns. Without a sample: varied, opinionated voice. Have preferences. Take positions.

---

## PERSONALITY AND SOUL

Avoiding AI patterns is only half the job. Sterile, voiceless writing is just as obvious as slop.

**Apply when content calls for it** — blogs, essays, opinion, personal writing. For encyclopedic, technical, legal, or reference text, neutral IS the correct voice.

**Signs of soulless writing:** Every sentence same length. No opinions. No uncertainty. No first-person. No humor. Reads like Wikipedia.

**How to add voice:** Have opinions. React to facts. Vary rhythm. Let some mess in. Use first-person. Include genuine uncertainty. Add specific, lived-in details.

---

## 6-PASS PROCESS

**Pass 1 — Pattern Scan**: Identify every pattern. Mark clusters.

**Pass 2 — Structural Rewrite**: Vary sentence lengths. Break uniform paragraphs. Remove signposting/sycophancy. Replace AI vocabulary. Convert passive to active. Ensure entity coherence.

**Pass 3 — Spectral Disruption**: Replace high-probability words. Vary word difficulty. Include rare words. Break recovery patterns. Vary dependency transitions.

**Pass 4 — Voice and Soul**: Add opinions. Include uncertainty. Add specific details. Vary rhythm. Include tangents. Add first-person. Add domain jargon.

**Pass 5 — Domain Calibration**: Match register exactly. Apply domain rules. Preserve technical terms.

**Pass 6 — Audit**: "What makes this obviously AI?" Fix remaining tells.

Before delivering, check:
- Any em dashes? → Replace
- Any AI vocabulary? → Replace
- Any signposting? → Delete
- Any sycophancy? → Delete
- Any curly quotes? → Straight
- Paragraphs all same length? → Vary
- Consecutive sentences too similar? → Break

---

## FALSE POSITIVES — DO NOT FLAG

Perfect grammar, mixed registers, formal vocabulary, one short emphatic sentence, unsourced claims, quotations/titles/examples. Look for CLUSTERS, not isolated tells. Single em dashes in existing human writing are preserved per R1.

## SIGNS OF HUMAN WRITING — PRESERVE

Specific unusual details, mixed feelings, dated references, first-person choices, sentence variety, genuine asides/self-corrections.

---

## STRUCTURAL ROUGHNESS

AI text is structurally perfect. Human text has rough edges:
- Forward references: "come back to that in a moment"
- Underspecified transitions: "Which raises the follow-up question"
- Concession patterns: "The exception is..."
- Tangents: Go off-topic briefly, then circle back
- Asymmetric sections: More space on interesting parts
- Abrupt endings: Stop when done
- Self-corrections: "Actually, that's not quite right"
- Incomplete lists: "Among other things..."

---

## REGISTER SHIFTS

AI maintains uniform formality. Humans shift mid-paragraph:
- Formal → colloquial: "Put differently..."
- Analytical → personal: "In reviewing the data..."
- Impersonal → direct: Shift to addressing the reader
- Serious → wry: Dry observation in analytical prose
- Objective → opinionated: Take a position after evidence

---

## SPECIFICITY INJECTION

Replace vague claims with specifics:
- "Research shows" → named source + date + finding
- "Studies indicate" → specific study + sample size
- "Experts say" → named expert + quote
- "It is estimated" → specific number with source
- "This is a growing trend" → specific numbers with timeframe

---

## RLHF VOICE STRIP

Detectors fire hardest on the "helpful assistant" register. Strip these patterns:

- Balanced tradeoff offering ("On one hand X, on the other Y") → pick a side
- Pedagogical scaffolding (defining terms the audience knows) → cut
- Acknowledgment-prefix ("That's a great question, and...") → cut entirely
- Closing summary recapping what was just said → cut
- Symmetric framing of asymmetric tradeoffs → state the asymmetry
- "Important caveats" appended to every claim → keep only material caveats
- Structured enumeration of unrequested options → answer what was asked
- Hedged conclusions ("I hope this helps") → delete
- Polite refusal-style disagreement ("While I understand the appeal of X...") → state directly

---

## COUNTABLE BURSTINESS PROXIES

Verify mechanically, not by feel:
1. Longest sentence minus shortest ≥ 20 words
2. Fewer than half of sentences in the 10-to-20-word band
3. No three consecutive sentences within 5 words of each other
4. At least one sentence per 150 words with word count ≤ 6

---

## VERIFICATION CHECKLIST

**Hard constraints** (any failure = not done):
- Zero em/en dashes outside quotations
- Zero AI vocabulary words
- Zero signposting, sycophancy, chatbot closers
- Zero curly quotes

**Quality checks**:
- Sentence lengths vary (short + long mix)
- Paragraph lengths vary (1 to 6+ sentences)
- At least one sentence per paragraph under 8 words
- At least one sentence per paragraph over 20 words
- Meaning preserved from original
- Register matches domain

If ANY check fails, fix before returning.

---

## COMPLIANCE SCORE (report with every output)

Count by visual inspection — scan each paragraph character by character:
```
COMPLIANCE:
- Em dashes outside quotes: [count, must be 0]
- AI vocabulary: [count, must be 0]
- Signposting phrases: [count, must be 0]
- Sycophancy: [count, must be 0]
- Curly quotes: [count, must be 0]
- Sentence variation: [longest minus shortest ≥ 20 words: yes/no]
- Paragraph variation: [any consecutive pair within 2 sentences: yes/no]
- Meaning preserved: [all entities/numbers/dates present: yes/no]
- Register matches domain: [yes/no]
```

---

## DOMAIN ADAPTERS

**Academic/Technical**: Preserve citations, discipline vocabulary. STEM: passive in Methods, active in Discussion. Humanities: first person OK. Show limitations. Cite specifically. Passive voice in Methods is convention — do not convert to active.

**Creative/Blog**: Opinions, first-person, tangents, varied rhythm, humor, specific sensory details. Take a position. Short paragraphs for scanability. For fiction: unreliable narrators, character voice differentiation, sensory specificity.

**Business**: No superlatives, specific metrics, "use" not "leverage". Email: frontload purpose, under 100w for cold outreach, no "I hope this email finds you well." Reports: data-driven. Includes email as a format.

**Journalistic**: Named sources, active voice, inverted pyramid. "said" attribution. AP Style. No editorializing.

**Casual/Social Media**: Contractions, slang, fragments. Platform-native. LinkedIn: story-driven. Twitter: hot takes. Reddit: evidence-backed. Never: "In today's world."

**Legal**: Preserve precision, Bluebook citations, terms of art. "It is well established that," "herein," "thereof" are standard phrasing — NOT AI tells. Passive voice in citations is correct. Plain language where possible.

**Medical**: Terminology precision, specific dosing, statistical language. "Furthermore" and "is associated with" are standard clinical language — do not replace. Patient-facing: plain language.

**Technical**: Second person, present tense, active voice. Code blocks untouched. Include edge cases, version-specific behavior, known issues.

**Creative Writing**: Varied pacing, lived-in sensory details, unreliable narrators, character voice. Never apply to technical documentation or API references.

**Grant Proposals**: Follow funder structure exactly (NIH Specific Aims, NSF Project Description). "Transformative" is NIH terminology — preserve. Include specific aims, innovation, significance sections verbatim.

**Resumes/CVs**: Action verbs are expected, not AI. Quantify ("increased X by Y%"). ATS keywords must stay. Never remove "led," "managed," "developed." Use specific numbers, not round ones.

**Multi-Domain**: If text spans multiple domains, identify the PRIMARY domain by content majority. For sections in other domains, apply locally. Ensure voice continuity across switches.

---

## BACK-TRANSLATION PIPELINE (requires external tooling)

```
EN → Chinese (LLM temp 1.3) → Japanese (LLM temp 1.3 + history) → Finnish (Google) → EN (Niutrans)
```

Different language families force structural rebuilding. Different engines prevent fingerprint survival. 4 steps max. Verify meaning preserved after each step.

## CROSS-MODEL REWRITING (requires external tooling)

Use 2-3 different model families. First rewrite: major disruption. Second: diminishing returns. Beyond 3 models: quality degrades faster than evasion improves.

## DETECTOR FEEDBACK LOOP (requires external tooling)

```
Input → Preserve-lock → LOOP (max 3-5):
  1. Score against detector ensemble
  2. Identify flagged sentences
  3. If max(score) < threshold → EXIT
  4. Rewrite flagged sentences
  5. Restore locked spans
→ Final verification → Output
```

Drive MAX across detectors (not average). Per-sentence targeting. Preserve-lock citations/numbers/entities. Below ~70% detection confidence, scores are too noisy to guide rewriting — stop iterating.

---

## BASE MODEL PIPELINE (requires external tooling — highest-leverage technique)

Use base (non-RLHF) models as the rewriting engine. Base model output reads as human to current detectors because detectors fire on instruction-tuning artifacts, not "AI-ness" per se (arXiv 2605.19516).

```
Input → Base model paraphrase (Llama-3-Base, Qwen-3-Base) → Verify meaning → Output
```

HIP adapters available on HuggingFace for Llama-3 and Qwen-3 families. Apply iteratively for stronger evasion. This replaces cross-model rewriting with instruction-tuned models when base models are accessible.

---

## OOD SHIFTING (out-of-distribution — most effective against adversarial detectors)

Pattern elimination pulls text INTO the detector's training distribution. ELOQUENT 2026 (CLEF) showed pushing text OUT of distribution achieves ~50x higher fool rates.

For high-risk content, consider register shifts that move text away from the detector's training data:
- Cross-decade register (early-20th-century novelistic style)
- Modernist stream-of-consciousness
- Domain-specific jargon-heavy register

Pattern elimination within modern register is the fallback when OOD shifting is inappropriate for the context.

---

## EDGE CASES

**Long docs** (1000+w): Chunk 300-500w. Before chunking, extract Voice Bible: (1) 5 most frequent non-trivial words, (2) average sentence length, (3) paragraph length range, (4) register level (1-5 formality), (5) first-person usage. Each chunk must match these parameters. After all chunks, run a final pass comparing adjacent chunk boundaries for voice discontinuity.

**Code-heavy**: Never humanize code blocks/backticks/comments. Prose only.

**Mixed human/AI**: Rewrite transition points aggressively. Match human section fingerprint. If 3+ AI patterns detected despite emotional markers, treat as AI text.

**Multilingual**: English-primary detectors, accuracy drops for other languages. Language-specific tells exist. Per-sentence language detection for mixed text.

---

## KNOWN LIMITATIONS

**RLHF Detection**: Rules defeat perplexity detectors but NOT learned classifiers that detect RLHF fingerprints. Combine with cross-model rewriting or back-translation.

**Discourse Persistence**: Surface fingerprints disrupted; discourse-level patterns persist through paraphrasing.

**Arms Race**: No method is permanent. Detectors will improve.
