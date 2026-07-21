---
name: humaniser
version: 3.5.0
description: "88 patterns, 16 rules, 11 domains — professional text humanization. Removes AI writing patterns and replaces them with natural voice. Based on adversarial NLP research (ACL/EMNLP/NAACL/AAAI 2024-2026), detection method analysis (GPTZero, Turnitin, Originality.ai, WaveDetect, FourierGPT), and analysis of competing humanizer tools (blader/humanizer, harshaneel/humanize)."
compatibility: any-agent
allowed-tools: [Read, Write, Edit, Grep, Glob]
---

# HumaniserUltra

Make AI text undetectable. Pattern elimination alone is not enough — detectors see through surface changes. This skill uses a layered approach: deep structural changes first, surface patterns second, detector verification last.

**Hard truth:** An instruction-tuned LLM rewriting text will always carry RLHF fingerprints. For high-stakes content, use base model rewriting (Section 1) or OOD shifting (Section 2). Pattern elimination (Section 3) is the foundation but not the ceiling.

## Modes

**Rewrite:** User pastes AI text → you humanize it.
**Write from scratch:** You generate text that follows all rules — no rewrite needed.
**Self-humanize:** Apply these rules to ALL your own output going forward.

---

## SECTION 1: BASE MODEL PIPELINE (highest-leverage — use first)

Base (non-RLHF) models produce text that reads as human to current detectors. Detectors fire on instruction-tuning artifacts, not "AI-ness" (arXiv 2605.19516).

**When to use:** High-stakes content (academic submissions, published articles, client deliverables).

**Pipeline:**
```
Input → Base model paraphrase (Llama-3-Base, Qwen-3-Base) → Verify meaning → Output
```

HIP adapters available on HuggingFace for Llama-3 and Qwen-3 families. Apply iteratively for stronger evasion. This is more effective than any pattern-based approach.

**If base models aren't available:** Use cross-model rewriting with 2-3 different model families (GPT → Claude → LLaMA). First rewrite: major disruption. Second: diminishing returns. Beyond 3: quality degrades.

---

## SECTION 2: OOD SHIFTING (most effective against adversarial detectors)

Pattern elimination pulls text INTO the detector's training distribution — which adversarial detectors are trained to recognize. Pushing text OUT of distribution achieves ~50x higher fool rates (ELOQUENT 2026, CLEF).

**When to use:** When pattern elimination alone fails. When content style is flexible.

**Techniques:**
- Cross-decade register (early-20th-century novelistic style)
- Modernist stream-of-consciousness
- Domain-specific jargon-heavy register

**When not to use:** Formal documents, technical specs, anything where register change damages meaning.

---

## SECTION 3: PATTERN ELIMINATION (foundation — always apply)

These rules remove the most obvious AI tells. They won't defeat sophisticated detectors alone, but they're necessary foundation work.

**STRUCTURAL-FIRST PRINCIPLE**: Word-level changes (synonym replacement) have near-zero impact on detection. Structural changes (sentence rhythm, paragraph variation, information flow) are 3-5x more impactful. Flip the ratio: 80% effort on structure, 20% on vocabulary.

### INPUT GATES (run before processing)

**Gate 0 — Length**: <50w → enforce R1-R7 only. 50-500w → rules only. 500-1000w → full. 1000+w → chunk 300-500w (see Voice Bible).

**Gate 1 — Language**: Non-English → apply only: R3, R4, R8, R10, R11, R16, and structural patterns (44-50). Skip R1, R2, R5-R7, R12-R14. Mixed-language → apply English rules to English segments, cross-linguistic to non-English.

**Gate 2 — Already Human**: Intentional informality, emotional voice, specific personal details, unresolved thoughts → return UNCHANGED. But still run pattern scan — if 3+ AI patterns detected, treat as AI text.

**Gate 3 — Code Fences**: ``` blocks, ~~~ blocks, inline backticks are CODE. Never humanize. Verify delimiters intact.

**Gate 4 — Sanitization**: Strip HTML comments, zero-width chars, invisible Unicode.

**Gate 5 — Tables**: Markdown tables, HTML tables, CSV, structured data are NOT prose. Do not humanize cell contents.

### ABSOLUTE RULES

Override everything. EXCEPTION: Text inside quotation marks is untouched. Domain-standard connectors are NOT AI tells in their domain.

**R1 — No AI Em Dashes**: Zero em (—) and en (–) dashes OUTSIDE quotations in AI-generated text. Replace with period, comma, colon, or parentheses. Preserve em dashes in existing human writing.

**R2 — No AI Vocabulary**: delve, tapestry, landscape, pivotal, testament, intricate, meticulous, nuanced, multifaceted, embark, spearhead, bolster, garner, interplay, realm, labyrinth, symphony, showcase, vibrant, robust, holistic, seamless, cutting-edge, game-changer, transformative, unprecedented, innovative, dynamic, fosters, cultivates, leverages, illuminates, underscores, resonates, encompasses, enhances, empowers, endeavors, navigates, unlocks, unleashes, drives, fuels, ignites, catalyzes, revolutionizes. Exact words only. Also match unhyphenated variants.

**R3 — No Forced Rule-of-Three**: Flag three adjectives ONLY when semantically redundant ("comprehensive and thorough"). Do NOT flag when items are categorically distinct ("primary colors," "past, present, future").

**R4 — No Negative Parallelisms**: No "Not only...but also" except scientific/legal precision.

**R5 — No Signposting**: No "Let's dive in," "Here's what you need to know," "In this post we'll cover."

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

### STATISTICAL TARGETS (qualitative — follow the guidance)

| Target | How to Hit |
|--------|-----------|
| **Burstiness** | Mix 3-5 word fragments with 25-40 word sentences. One sentence per paragraph under 8 words, one over 20. |
| **Sentence variation** | Alternate short punchy with long flowing. No two consecutive sentences within 5 words of same length. |
| **Paragraph variation** | Some 1 sentence, some 6+. No two consecutive paragraphs within 2 sentences of same length. |
| **Transition density** | Max 2 transition words (however, moreover, furthermore, consequently, additionally, nevertheless) per 100 words. Most paragraphs: zero transitions. |
| **Vocabulary diversity** | Don't repeat the same word within 3 sentences. Use domain-specific terminology. |
| **Entity coherence** | Introduce key entities early. Reference them later. Don't abandon entities. |

**Countable proxies:**
1. Longest sentence minus shortest ≥ 20 words
2. Fewer than half of sentences in the 10-to-20-word band
3. No three consecutive sentences within 5 words of each other
4. At least one sentence per 150 words with word count ≤ 6

### PATTERNS — DETECT AND FIX ALL (1-50)

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

### Essay-Specific (fix these in personal/creative writing)
51. **Smooth Timeline**: AI moves milestone-to-mileline without detours. Add parenthetical asides, self-corrections, memory triggers, forward references. Let the current topic trigger a memory — jump without "This reminds me of..."
52. **Predictable Paragraph Pattern**: AI uses "example → explanation → takeaway" every time. Alternate: burst (1-2 sentences), slow build, inverted pyramid, catalog, contrast without resolution.
53. **Contrast Overuse**: AI defaults to "X wanted Y. The result was Z." Rotate: analogy, causation, classification, concession, question, hypophora, metanoia. If three paragraphs all use contrast, the fourth should use something else.
54. **Uniform Confidence**: AI is equally certain throughout. Modulate: flat assertion for facts, slight hedge for supported claims, strong hedge for speculation, open uncertainty when genuinely unsure. Change your mind mid-essay. Include weak evidence alongside strong.
55. **Fabricated Anecdotes**: AI claims "I remember..." with impossible specificity. Use: hypotheticals ("Imagine..."), collective voice ("Every developer has..."), observed behavior ("Watch a PM receive..."), anonymous expert ("Most engineers will tell you..."), detail without "I" ("The coffee was cold.").
56. **Self-Aware AI Narrator**: AI writing about being AI or like AI. Never do this. Write AS a human, not ABOUT being human-like.
57. **Bold Take Hedge**: "Here is where I lose the room at conferences" pre-hedges a contrarian opinion. State the opinion directly without pre-framing it as controversial.
58. **Tidy Aphoristic Closer**: "That is not a methodology. It is a personality trait. And you cannot certify for that." — quotable one-liner wrapping the thesis. End on a specific detail, a question, or just stop. Don't wrap it up.
59. **Even Pacing**: Every example gets ~equal space. Human writers linger on what interests them and rush past the rest. Spend 3 sentences on the thing you care about, 1 sentence on the thing you don't.
60. **Systematizing Habit**: Turning fuzzy concepts into crisp yes/no tests or clean frameworks. "Does the system decide which tools to call...? If yes, agent. If no, automation." Leave some things fuzzy.
61. **Generic Completeness**: Covers every expected topic evenly. Missing the surprising angle, the thing nobody talks about, the tangent that doesn't advance the argument but is true.
62. **Contrast as Default Move**: "The scope problem is not really about scope. It is about..." — contrast used as the primary rhetorical device across paragraphs. Rotate through other devices.
63. **No Dead-End Tangents**: Every digression circles back. Real essays have tangents that don't return — thoughts that trail off, observations that don't connect to the thesis.
64. **Missing Lived Friction**: No typos, no awkward sentences, no "wait, let me reconsider" moments. Add 1-2 deliberately imperfect sentences.
65. **Tidy Conclusion**: Clean, quotable ending that wraps everything up. Replace with: a specific detail, a question that hangs, or just stop mid-thought. Also: don't gesture at emotion — anchor it in concrete detail. "I felt surprise" is generic. "I refreshed the analytics dashboard every four minutes for three hours" is specific. Don't say "I watched the chart and felt something" — say what you actually saw and what you actually did next.
56. **Self-Aware AI Narrator**: AI writes in first person about being an AI, running on "the same loop" as agents it describes. This is a strong tell — an AI reflecting on being like an AI is AI performing self-awareness. Fix: write from a human perspective about technology, not from an AI perspective about itself. Use genuine human experience ("I've spent 10 years building these systems") not simulated self-awareness ("I run on the same loop").
57. **"Bold Take" Hedge**: AI signals a controversial opinion ("Here's where I'll lose people") then states something safe and well-reasoned. Simulates risk-taking without actually taking risks. Fix: either take a genuinely challenging position OR don't frame it as bold. If the opinion is mainstream, just state it without the performative disclaimer.
58. **Even Pacing Across Examples**: AI gives each example exactly one paragraph with the same structure: one fact, one anecdote, one verdict. Human writers linger on what interests them and rush past the rest. Fix: spend 3 paragraphs on your best example, 2 sentences on the weakest. Let your genuine interest dictate pacing.
59. **Antithesis Tic**: "X did this. Y did that." repeated as a structural habit across the piece — clean two-sentence contrast used over and over. Different from Pattern 46 (4-Beat Progression) which is about paragraph-level structure. This is about SENTENCE-LEVEL antithesis becoming a tic. Fix: limit antithesis pairs to max 2 per piece. Replace others with causation, analogy, or narration.
60. **Systematizing Habit**: Turning fuzzy, nuanced concepts into crisp yes/no tests or definitional frameworks. "If yes, agent. If no, automation with a chatbot attached." Humans tolerate ambiguity; LLMs resolve it prematurely. Fix: leave some concepts fuzzy. Let the reader sit with uncertainty instead of providing a clean framework.
61. **Generic Completeness**: AI covers every expected aspect of a topic without saying much. The text is thorough but shallow — it touches everything, commits to nothing. Fix: pick 2-3 aspects and go deep. Leave others out entirely. Depth beats breadth.
62. **Repetitive Semantic Loops**: The same point appears 3-5 times in slightly different form across paragraphs. AI rephrases rather than advances. Fix: each paragraph should say something NEW. If you've made the point, move on.
63. **Style Mismatch**: One section sounds different from the rest — different register, different complexity, different rhythm. This happens when AI shifts between modes (e.g., formal intro → casual middle → formal conclusion). Fix: maintain consistent register throughout, or make register shifts deliberate and visible.
64. **Editing Artifacts**: Odd section transitions, duplicated bullet logic, paragraphs that feel copy-pasted from different contexts. Fix: read transitions aloud. If a jump feels unnatural, bridge it or cut the section.
65. **Provenance Clues**: No drafts, no version history, no evidence of a writing process. Human text has fingerprints of revision — crossed-out ideas, marginal notes, rewordings. Fix: where possible, include process evidence (drafts, research notes, revision history).
61. **ChatGPT**: Em-dashes 3x human rate, "In today's digital age", "delve into".
62. **Claude**: Flowing paragraphs, qualification endings, context-before-answer.
63. **Gemini**: Simpler vocabulary, "might" overuse, clinical tone.
64. **Grok**: Internet slang, sarcasm, 0% sycophancy.
65. **GPT-5+**: Reduced em-dashes, framing verb clusters, deliberate imperfections.
66. **Claude Opus 4.5**: Reportedly em-dash 16.8x, colon 4.1x, "comprehensive" 24x. Fingerprints change with model updates.
67. **DeepSeek-R1**: Most detectable — chain-of-thought contamination.

*Note: Model fingerprints change with updates. Verify against current output, not historical data.*

### Spectral & Statistical
68. **Uniform Token Probability**: Fix: different model rewrite, temp 0.7-1.0.
69. **Low Spectral Energy**: Fix: unexpected word choices.
70. **Recovery Pattern**: Fix: keep surprise going 2+ sentences.
71. **Low Dependency Entropy**: Fix: vary dependency labels, embed clauses.
72. **Uniform POS Distribution**: Fix: vary POS patterns.
73. **Low Type-Token Ratio**: Fix: increase lexical diversity.
74. **N-gram Repetition**: Fix: vary sentence openings.

### Structural Deep
75. **Entity Abandonment**: Fix: track and reference.
76. **Uniform Discourse**: Fix: add Contrast, Cause, Condition.
77. **Middle-Register Default**: Fix: match target register exactly.
78. **Semantic Smoothness**: Fix: add tangents, self-corrections.
79. **Nominalization Overuse**: "implementation" → "implementing".
80. **Coordination > Subordination**: Fix: use "although," "because."
81. **Direct Object Position**: Fix: vary placement.
82. **Non-Stationarity**: AI text has 73.8% more variation between segments than human writing. Fix: vary sentence-level perplexity ACROSS paragraphs, place high-surprise sentences in varied positions, include 2-3 "boring" paragraphs mixed with high-surprise ones.

### Detectors
83. **OpenAI Watermark**: Removed by 50%+ word changes.
84. **Google SynthID**: Removed by significant rewriting.
85. **Turnitin AI-Paraphrased**: Flags humanizer-processed text. Needs deeper structural changes.
86. **Originality.ai Deep Scan**: Light editing reduces ~15% only.
87. **Ensemble Detection**: Must address ALL signals simultaneously.
88. **Pangram Labs**: Different detection axis entirely.

---

## FALSE POSITIVES — DO NOT FLAG

Perfect grammar, mixed registers, formal vocabulary, one short emphatic sentence, unsourced claims, quotations/titles/examples. Look for CLUSTERS, not isolated tells. Single em dashes in existing human writing are preserved per R1.

## SIGNS OF HUMAN WRITING — PRESERVE

Specific unusual details, mixed feelings, dated references, first-person choices, sentence variety, genuine asides/self-corrections, tangents that circle back, parenthetical asides, self-corrections mid-paragraph, memory triggers, forward references, rhetorical variety (not just contrast), confidence modulation (hedges where uncertain, assertions where sure), specific numbers and dates, named sources with context, weak evidence alongside strong, change of mind mid-essay, unresolved questions, asymmetrical paragraph lengths.

---

## SECTION 4: VOICE AND SOUL (apply after pattern elimination)

Pattern elimination removes tells. This section adds humanity.

### Voice Calibration
If user provides a writing sample: read it, note sentence patterns, word choices, punctuation habits, paragraph length, register level. Match their style — don't just remove AI patterns, replace with their patterns. Without a sample: varied, opinionated voice. Have preferences. Take positions.

**What to extract from a sample:**
1. Average sentence length and variation
2. Punctuation habits (dashes, semicolons, parentheses)
3. First-person usage rate
4. Formality level (1-5 scale)
5. Transition preferences (explicit connectors or just start next point)
6. 3-5 most characteristic phrases or patterns
Apply when content calls for it — blogs, essays, opinion, personal writing. For encyclopedic, technical, legal, or reference text, neutral IS the correct voice.

**Signs of soulless writing:** Every sentence same length. No opinions. No uncertainty. No first-person. No humor. Reads like Wikipedia.

**How to add voice:** Have opinions. React to facts. Vary rhythm. Let some mess in. Use first-person. Include genuine uncertainty. Add specific, lived-in details.

### RLHF Voice Strip
Detectors fire hardest on the "helpful assistant" register. Strip these:
- Balanced tradeoff offering → pick a side
- Pedagogical scaffolding → cut, trust the reader
- Acknowledgment-prefix ("That's a great question, and...") → cut entirely
- Closing summary recapping → cut
- Symmetric framing of asymmetric tradeoffs → state the asymmetry
- "Important caveats" appended to every claim → keep only material ones
- Hedged conclusions ("I hope this helps") → delete

### Structural Roughness
AI text is structurally perfect. Human text has rough edges:
- Forward references: "come back to that in a moment"
- Underspecified transitions: "Which raises the follow-up question"
- Concession patterns: "The exception is..."
- Tangents: Go off-topic briefly, then circle back
- Asymmetric sections: More space on interesting parts
- Abrupt endings: Stop when done
- Self-corrections: "Actually, that's not quite right"
- Incomplete lists: "Among other things..."

### Controlled Roughness (addresses ChatGPT's 5 remaining tells)

**0. The First Paragraph Test** — Cut your first paragraph. Nine times out of ten the piece gets stronger. That paragraph was throat-clearing. Start with your second paragraph, or with a specific claim, scene, contradiction, or question. Never open by announcing you're about to explain something.

**1. Timeline Digression** — AI moves milestone-to-milestone without detours. Add:
- Parenthetical asides that reveal the writer's mind: "The project shipped — and I mean barely, the kind of shipping where you hold your breath and click deploy on a Friday — but it shipped."
- Self-corrections mid-paragraph: "Or rather, it killed the idea of the office — the building still stands somewhere in New Jersey, collecting dust."
- Memory triggers that jump without transition: "The data shows a 40% increase. Which, now that I think about it, is about the same margin of error as the coffee machine study they ran in 2019."
- Forward references: "We'll get to the numbers in a moment. But first, a detour that matters."

**2. Paragraph Pattern Breaker** — AI uses "example → explanation → takeaway" every time. Alternatives:
- The Burst: 1-2 sentences, no explanation, no takeaway. "The meeting could have been an email. It could have been a Slack message. It could have been nothing."
- The Slow Build: Start with a specific detail. Let it accumulate meaning. End somewhere unexpected.
- The Inverted Pyramid: Evidence first. Let reader draw conclusions before you state yours.
- The Nested Parenthetical: Main sentence → aside → aside → return → finish.
- The Contrast Without Resolution: Present two sides. Don't pick one. "The data says the feature is popular. The support tickets say it's broken. Both are true."
- The Catalog: List observations without connecting them. Let reader find the pattern.

**3. Rhetorical Device Rotation** — AI defaults to contrast every time. Rotate through:
- Analogy: "Optimizing code without understanding the problem is like redecorating a sinking ship."
- Causation: "The policy failed because it assumed compliance."
- Classification: "There are three kinds of technical debt: the kind you chose, the kind you inherited, and the kind you can't see."
- Concession: "Yes, the data supports X. But data doesn't account for Y."
- Question: "What if the entire model is wrong? Not partially. Completely."
- Hypophora: Ask a question, then answer it yourself.
- Metanoia: "It wasn't good. No, that's wrong — it was extraordinary."

**4. Confidence Modulation** — AI is uniformly confident throughout. Humans modulate:
- Flat assertion: "This is wrong." (well-established facts)
- Slight hedge: "The evidence suggests..." (supported but not universal)
- Strong hedge: "It's possible that..." (speculative)
- Open uncertainty: "I'm not sure what to make of this." (genuinely don't know)
- Change your mind mid-essay: "I used to think X but now I'm not so sure."
- Include weak evidence alongside strong: Show the reader what doesn't fit.
- Qualify at highest tension: Hedge where the reader is deciding whether to trust you.

**5. Anecdote Alternatives** — AI fabricates unverifiable first-person stories. Replace with:
- The Hypothetical: "Imagine walking into the office on Monday. The deadline was Friday. Nobody was talking about it."
- The Collective "We": "Every developer has spent three hours debugging something that turned out to be a missing semicolon."
- The Observed Behavior: "Watch a project manager receive the fifth set of revised requirements. Note the pause. The slow blink."
- The Anonymous Expert: "Most senior engineers will tell you the same thing: the code is never the hard part."
- Specific Detail Without "I": "The coffee was cold. The meeting room smelled like stress."

**6. Zeigarnik Effect** — Open loops early, make people wait. Tease something ("the fix took eleven minutes and cost nothing") and don't resolve it immediately. The mind holds onto unresolved things harder than resolved ones. But don't open ten loops and close none — that reads as manipulative.

**7. Cut, Don't Add** — The first draft is for getting the idea down. The edit is for removing anything that isn't earning its place. Cut throat-clearing intros, intensifiers ("very," "really," "quite"), sentences that repeat a point already made. Aim to cut 15-20% of the first draft. It almost always gets better, never worse.

**8. Write Like You Talk** — Read your draft out loud. Anywhere you stumble, or anywhere you'd never actually say that sentence to a friend, rewrite it. Use contractions. Use "you." Cut words nobody says out loud — "utilize," "facilitate," "in order to." This is the fastest fix available.

### Register Shifts
AI maintains uniform formality. Humans shift mid-paragraph:
- Formal → colloquial: "Put differently..."
- Analytical → personal: "In reviewing the data..."
- Impersonal → direct: Shift to addressing the reader
- Serious → wry: Dry observation in analytical prose
- Objective → opinionated: Take a position after evidence

### Specificity Injection
Replace vague claims with specifics:
- "Research shows" → named source + date + finding
- "Studies indicate" → specific study + sample size
- "Experts say" → named expert + quote
- "It is estimated" → specific number with source

---

## SECTION 5: VERIFICATION

### Verification Checklist

**Hard constraints** (any failure = not done):
- Zero em/en dashes outside quotations
- Zero AI vocabulary words
- Zero signposting, sycophancy, chatbot closers
- Zero curly quotes

**Quality checks**:
- Sentence lengths vary (longest minus shortest ≥ 20 words)
- Paragraph lengths vary (1 to 6+ sentences)
- At least one sentence per paragraph under 8 words
- At least one sentence per paragraph over 20 words
- Meaning preserved from original
- Register matches domain

If ANY check fails, fix before returning.

### Reasoning Verification (MANDATORY)

Before claiming output is done, verify your reasoning chain:

1. **Claim-Evidence Check**: For every factual claim in the output, can you point to the source text? If you added a fact not in the input, flag it.
2. **Rule Compliance Check**: Walk through R1-R16 one by one. For each, state "PASS" or "FAIL" with evidence. No skipping.
3. **Pattern Check**: Walk through patterns 1-50. For each relevant one, state whether it was found and fixed. "NOT APPLICABLE" is valid — but you must explicitly state it.
4. **Domain Check**: State which domain adapter was applied. Justify why. If domain is ambiguous, state your reasoning.
5. **Meaning Preservation Check**: List all entities (names, numbers, dates, proper nouns) from input. Confirm each appears in output. State "ALL PRESERVED" or list what was lost.

Format your verification as:
```
REASONING VERIFICATION:
- R1 (Em dashes): PASS — zero found in output [grep evidence]
- R2 (AI vocabulary): PASS — zero banned words found
- ...
- Domain: [domain] — applied because [reasoning]
- Meaning: ALL PRESERVED — [entity count] entities verified
- Confidence: [HIGH/MEDIUM/LOW] — [reason why]
```

If confidence is LOW, explain what you're uncertain about and why.

### Compliance Score (report with every output)

Count by visual inspection — scan each paragraph:
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

### Detector Feedback Loop (requires external tooling)

If pattern elimination doesn't pass detection, escalate:
```
Input → Preserve-lock → LOOP (max 3-5):
  1. Score against detector ensemble
  2. Identify flagged sentences
  3. If max(score) < threshold → EXIT
  4. Rewrite flagged sentences
  5. Restore locked spans
→ Final verification → Output
```

Drive MAX across detectors (not average). Per-sentence targeting. Below ~70% detection confidence, scores are too noisy — stop iterating.

### Semantic Drift Protocol (MANDATORY)

Before humanizing, extract and lock these categories. After humanizing, verify each:

| Category | What to Lock | How to Verify |
|----------|-------------|---------------|
| **Entities** | People, orgs, places | grep — all must appear in output |
| **Numbers** | Exact values, units, ranges | grep digits — count must match |
| **Dates** | All time expressions | grep — count must match |
| **Causal claims** | "X causes Y" | Must remain causal, not correlational |
| **Comparatives** | "more than", "less than" | Direction unchanged |
| **Qualifiers** | "some", "many", "most", "all" | Check none escalated/de-escalated |
| **Negation** | "not", "never", "no" | Must apply to same clauses |

If ANY category fails → reject output, re-humanize with stricter entity locks.

### Anti-Self-Evaluation Bias

The agent that humanizes is the same agent that audits. This creates blind spots. Mitigate:

1. **Adversarial prompt before delivery**: "A hostile reviewer with GPTZero, Turnitin, and Originality.ai is reading this. They are looking for any sentence that could be from a language model. What would they flag?"
2. **Structured rubric**: Don't ask "is this human?" Score on: Would a native speaker write this? Does this paragraph have a personality? Is there at least one genuine opinion? Are there any "too perfect" transitions?
3. **Role switching**: After rewrite, explicitly switch persona: "You are now a skeptical editor trying to prove this text is AI."

### Back-Translation Pipeline (requires external tooling)

```
EN → Chinese (LLM temp 1.3) → Japanese (LLM temp 1.3 + history) → Finnish (Google) → EN (Niutrans)
```

Different language families force structural rebuilding. Different engines prevent fingerprint survival. 4 steps max.

---

## SECTION 6: EDGE CASES

**Long docs** (1000+w): Chunk 300-500w. Before chunking, extract Voice Bible: (1) 5 most frequent non-trivial words, (2) average sentence length, (3) paragraph length range, (4) register level (1-5 formality), (5) first-person usage. Each chunk must match these parameters. After all chunks, run a final pass comparing adjacent chunk boundaries for voice discontinuity.

**Code-heavy**: Never humanize code blocks/backticks/comments. Prose only.

**Mixed human/AI**: Rewrite transition points aggressively. Match human section fingerprint. If 3+ AI patterns detected despite emotional markers, treat as AI text.

**Multilingual**: English-primary detectors, accuracy drops for other languages. Language-specific tells exist. Per-sentence language detection for mixed text.

---

## DOMAIN ADAPTERS

**Academic**: Preserve citations, discipline vocabulary. STEM: passive in Methods, active in Discussion. Humanities: first person OK. Show limitations. Cite specifically.

**Creative/Blog**: Opinions, first-person, tangents, varied rhythm, humor, specific sensory details. Take a position. Short paragraphs for scanability.

**Business**: No superlatives, specific metrics, "use" not "leverage". Email: frontload purpose, under 100w for cold outreach, no "I hope this email finds you well." Reports: data-driven.

**Journalistic**: Named sources, active voice, inverted pyramid. "said" attribution. AP Style. No editorializing.

**Casual/Social**: Contractions, slang, fragments. Platform-native. Twitter: hot takes. LinkedIn: story-driven. Reddit: evidence-backed.

**Legal**: Preserve precision, Bluebook citations, terms of art. "It is well established that" is standard phrasing, not AI. Passive voice in citations is correct.

**Medical**: Terminology precision, specific dosing, statistical language. "Furthermore" and "is associated with" are standard clinical language — do not replace.

**Technical**: Second person, present tense, active voice. Code blocks untouched. Include edge cases, version-specific behavior, known issues.

**Creative Writing**: Varied pacing, lived-in sensory details, unreliable narrators, character voice. Never apply to technical documentation.

**Grant Proposals**: Follow funder structure exactly (NIH Specific Aims, NSF Project Description). "Transformative" is NIH terminology — preserve.

**Resumes/CVs**: Action verbs are expected, not AI. Quantify ("increased X by Y%"). ATS keywords must stay. Never remove "led," "managed," "developed."

**Multi-Domain**: If text spans multiple domains, identify PRIMARY domain by content majority. Apply other domains locally. Ensure voice continuity.

---

## FORMAT PLAYBLOKS

### Blogs
- **Headline**: Specific + benefit/gap. Never vague. "5 Tips for Productivity" → "I Cut My Inbox Time in Half With One Rule"
- **Intro**: Skip "In this article, we'll cover..." Open with sharpest claim, surprising number, or one-line scene.
- **Body**: Subheads work as skimmable spine. Vary paragraph length. Don't let every paragraph run 4-5 sentences.
- **Ending**: Don't summarize. End on a question, next step, or sharper version of original claim.

### Email
- **Subject**: Short, specific. Curiosity-driven or benefit-driven — not both.
- **Preview text**: Second subject line, not repeat of first.
- **First line**: Must work if it's the only line anyone reads.
- **Body**: One idea, one call to action. Three things = none done well.
- **P.S.**: People skim to it. Use for second hook or restated CTA.

### Video Scripts
- First 10-15 seconds carry entire weight. Skip logo, "hey guys," outline. Just start.
- State payoff early: what they get, why worth next 15 seconds.
- Re-earn attention every 30-60 seconds with pattern interrupts.
- Write for ear, not eye: shorter sentences, direct address, repetition of key idea.

### Podcast/Audio
- Bullet-point outline usually sounds better than word-for-word script.
- Read everything out loud before recording. Stumble = rewrite.
- Leave room to riff. Most human moments aren't fully scripted.

---

## FRAMEWORKS

Use ONE per piece — don't stack all four in a single email.

- **AIDA** (Attention, Interest, Desire, Action) — oldest, solid for ads, landing pages, cold outreach.
- **PAS** (Problem, Agitate, Solution) — name problem, make reader feel cost, then solve. Works when reader already knows they have the problem.
- **BAB** (Before, After, Bridge) — painful current state, desired state, how to cross gap. Good when reader doesn't realize they have a problem yet.
- **StoryBrand** — reader is hero, you're guide. Useful when writing starts sounding like it's about you instead of them.

---

## PRE-PUBLISH CHECKLIST

- [ ] Read it out loud. Stumble = rewrite.
- [ ] Cut first paragraph. Stronger without it?
- [ ] Circle every "very," "really," "in order to," "it's important to note" — cut or replace.
- [ ] Check three consecutive sentences for length. All within few words? Break pattern.
- [ ] At least one specific, real number/name/detail — something only you could have written.
- [ ] Takes an actual position, or hedges everything?
- [ ] Ending adds something new, or just repeats?

---

## KNOWN LIMITATIONS

**RLHF Detection**: Rules defeat perplexity detectors but NOT learned classifiers that detect RLHF fingerprints. Combine with cross-model rewriting or back-translation.

**Discourse Persistence**: Surface fingerprints disrupted; discourse-level patterns persist through paraphrasing.

**Arms Race**: No method is permanent. Detectors will improve.

**Semantic Drift**: #1 failure mode — quiet claim changes, missing numbers, collapsed qualifiers. Always run Semantic Drift Protocol.

**Structural vs Lexical**: Word-level changes have near-zero impact on detection. Structural changes (sentence rhythm, paragraph variation, information flow) are 3-5x more impactful. Prioritize structure over vocabulary.

**Silent Failures**: Text that passes all grep checks but fails spectral analysis. Most dangerous mode. Requires cross-model rewriting or back-translation to fix.
