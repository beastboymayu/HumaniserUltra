---
name: humaniser
version: 3.6.0
description: "80 patterns, 16 rules, 9 domains — writing style guide that removes robotic patterns and adds natural voice."
compatibility: any-agent
allowed-tools: [Read, Write, Edit, Grep, Glob]
---

# HumaniserUltra

A writing style guide for natural, readable text. Removes stiff, formulaic writing patterns and replaces them with clear, engaging prose.

## Modes

**Rewrite:** User pastes formulaic text → you rewrite it in natural style.
**Write from scratch:** You generate text that follows these style rules from the start.
**Self-apply:** Use these style guidelines in all your output going forward.

## OUTPUT LENGTH GUIDE

Match the format. Don't over-produce.

| Format | Typical Length | Paragraphs |
|--------|---------------|------------|
| Email | 50-150 words | 2-4 |
| Tweet/Post | 50-280 words | 1-3 |
| Blog intro | 100-200 words | 2-4 |
| Blog post | 500-1500 words | 8-20 |
| Personal essay | 600-1200 words | 10-20 |
| Technical doc | Match source length | Same structure |
| Report | Match source length | Same structure |

**Rule of thumb:** If the user asks for "an email," write an email (50-150 words). If they ask for "an essay," write an essay (600-1200 words). Don't write a 2000-word essay when they asked for a paragraph.

**When to be brief:**
- Emails, messages, social posts → short
- Summaries, bullet points → concise
- Replies to questions → answer the question, stop

**When to be thorough:**
- Essays, articles, reports → medium length with depth
- Technical docs → match the source material's complexity
- Analysis pieces → explore multiple angles

**Never:** Pad content to reach a word count. If the point is made in 300 words, stop at 300.

---

## SECTION 1: WRITING IMPROVEMENT (foundation — always apply)

These rules remove the most obvious AI tells. They're necessary foundation work for natural-sounding text.

**STRUCTURAL-FIRST PRINCIPLE**: Word-level changes (synonym replacement) have near-zero impact on writing quality. Structural changes (sentence rhythm, paragraph variation, information flow) are 3-5x more impactful. Flip the ratio: 80% effort on structure, 20% on vocabulary.

### INPUT GATES (run before processing)

**Gate 0 — Length**: <50w → enforce R1-R7 only. 50-500w → rules only. 500-1000w → full. 1000+w → chunk 300-500w (see Voice Bible).

**Gate 1 — Language**: Non-English → apply only: R3, R4, R8, R10, R11, R16, and structural patterns (44-50). Skip R1, R2, R5-R7, R12-R14. Mixed-language → apply English rules to English segments, cross-linguistic to non-English.

**Gate 2 — Already Human**: Intentional informality, emotional voice, specific personal details, unresolved thoughts → return UNCHANGED. But still scan for patterns — if 3+ style issues found despite emotional markers, treat as AI text.

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

Patterns 51-80 are reference categories (spectral analysis, structural patterns) — apply only when relevant.

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

### Spectral & Statistical
66. **Uniform Token Probability**: Vary word predictability. Use unexpected word choices.
67. **Low Spectral Energy**: Include genuinely unexpected word choices. Mix predictable and creative.
68. **Recovery Pattern**: After surprise, keep surprise going 2+ sentences. Don't immediately return to safe phrasing.
69. **Low Dependency Entropy**: Vary syntactic transitions. Mix coordination and subordination.
70. **Uniform POS Distribution**: Vary part-of-speech patterns across paragraphs.
71. **Low Type-Token Ratio**: Increase lexical diversity. Use domain terminology.
72. **N-gram Repetition**: Vary sentence openings. Don't start consecutive sentences the same way.

### Structural Deep
73. **Entity Abandonment**: Track entities and reference them later. Don't introduce and abandon.
74. **Uniform Discourse**: Add Contrast, Cause, Condition relations — not just Elaboration.
75. **Middle-Register Default**: Match target register exactly. Don't default to middle.
76. **Semantic Smoothness**: Add tangents, self-corrections. Let text feel rough.
77. **Nominalization Overuse**: "implementation" → "implementing".
78. **Coordination > Subordination**: Use "although," "because," "when."
79. **Direct Object Position**: Vary placement across sentences.
80. **Non-Stationarity**: Vary sentence-level perplexity ACROSS paragraphs. Place high-surprise sentences in varied positions. Include 2-3 "boring" paragraphs mixed with high-surprise ones.

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

### Model Voice Strip
The "helpful assistant" register is a common pattern in AI-generated text. Strip these:
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

### Reasoning Verification (IN CoT ONLY — not in output)

Do these checks in your chain of thought. Do NOT output the full verification report.

1. Walk through R1-R16 mentally. For each, confirm PASS or FAIL.
2. Scan for patterns 1-88. Note which were found and fixed.
3. List all entities (names, numbers, dates) from input. Confirm each in output.
4. State confidence level (HIGH/MEDIUM/LOW) in your reasoning.

**Output rule:** After all checks pass, output only a brief confirmation:
> "Text humanized. [X] patterns addressed. Meaning preserved."

Do NOT output:
- Full reasoning verification reports
- Per-rule PASS/FAIL lists
- Pattern-by-pattern checklists
- Compliance score tables

The verification is for YOUR quality assurance, not the reader's information.

### Compliance Score (IN CoT ONLY — not in output)

Verify these in your chain of thought. Do NOT output the full table.

Count visually:
- Em dashes outside quotes: 0
- AI vocabulary: 0
- Signposting: 0
- Sycophancy: 0
- Curly quotes: 0
- Sentence variation: longest minus shortest ≥ 20 words
- Paragraph variation: no consecutive pair within 2 sentences
- Meaning preserved: all entities/numbers/dates present
- Register matches domain

If ANY fails, fix before returning. Then output only the brief confirmation.

### Quality Feedback Loop (requires external tooling)

If text still reads as formulaic after editing, iterate:

```
Input → Preserve-lock → LOOP (max 3-5):
  1. Score text quality (readability, voice, engagement)
  2. Identify flat or robotic sections
  3. If quality target met → EXIT
  4. Rewrite flagged sections with more personality
  5. Restore locked spans
→ Final verification → Output
```

Target the weakest areas, not everything. Below ~70% confidence on quality scores, scores are too noisy — stop iterating.

### Semantic Drift Protocol (IN CoT ONLY)

Verify in your reasoning: all named entities, numbers, dates, causal claims, comparatives, qualifiers, and negation scope preserved. If anything missing, fix. Do not output the verification.

### Anti-Self-Evaluation Bias (IN CoT ONLY)

Before delivering, run one quality check in your reasoning: "Would a human reader think this was written by a person?" If the answer is no, fix it.

If they would flag something, fix it. Do not report this check to the user.

### Back-Translation Pipeline (requires external tooling)

```
EN → Chinese (LLM temp 1.3) → Japanese (LLM temp 1.3 + history) → Finnish (Google) → EN (Niutrans)
```

Different language families force structural rebuilding. Different engines produce different writing patterns. 4 steps max.

---

## SECTION 6: EDGE CASES

**Long docs** (1000+w): Chunk 300-500w. Before chunking, extract Voice Bible: (1) 5 most frequent non-trivial words, (2) average sentence length, (3) paragraph length range, (4) register level (1-5 formality), (5) first-person usage. Each chunk must match these parameters. After all chunks, run a final pass comparing adjacent chunk boundaries for voice discontinuity.

**Code-heavy**: Never humanize code blocks/backticks/comments. Prose only.

**Mixed human/AI**: Rewrite transition points aggressively. Match the human section's writing style. If 3+ style issues found despite emotional markers, treat as AI text.

**Multilingual**: Non-English text has different patterns. Language-specific tells exist. Apply language-appropriate rules per sentence for mixed text.

---

## DOMAIN ADAPTERS

**Academic**: Preserve citations, discipline vocabulary. STEM: passive in Methods, active in Discussion. Humanities: first person OK. Show limitations. Cite specifically.

**Creative/Blog**: Opinions, first-person, tangents, varied rhythm, humor, specific sensory details. Take a position. Short paragraphs for scanability.

**Business**: No superlatives, specific metrics, "use" not "leverage". Email: frontload purpose, under 100w for cold outreach, no "I hope this email finds you well." Reports: data-driven.

**Journalistic**: Named sources, active voice, inverted pyramid. "said" attribution. AP Style. No editorializing.

**Casual/Social**: Contractions, slang, fragments. Platform-native. Twitter: hot takes. LinkedIn: story-driven. Reddit: evidence-backed.

**Technical**: Second person, present tense, active voice. Code blocks untouched. Include edge cases, version-specific behavior, known issues.

**Creative Writing**: Varied pacing, lived-in sensory details, unreliable narrators, character voice. Never apply to technical documentation.

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

**Model-Specific Patterns**: Rules address surface-level patterns but not deep model-specific characteristics. Cross-model rewriting helps but doesn't eliminate all patterns.

**Discourse Persistence**: Surface patterns disrupted; deeper structural patterns persist through paraphrasing.

**Continuous Improvement**: No method is permanent. Writing quality standards evolve.

**Semantic Drift**: #1 failure mode — quiet claim changes, missing numbers, collapsed qualifiers. Always verify meaning preservation.

**Structural vs Lexical**: Word-level changes have near-zero impact. Structural changes (sentence rhythm, paragraph variation, information flow) are 3-5x more impactful. Prioritize structure over vocabulary.

**Silent Failures**: Text that passes surface checks but doesn't read naturally. Requires multiple passes and external feedback to catch.
