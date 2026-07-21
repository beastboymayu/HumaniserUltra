# Advanced Writing Techniques (optional)

These techniques require external tooling or are for specific use cases. Only load when needed.

## Quality Feedback Loop

If text still reads as formulaic after editing, use iterative quality improvement:

```
Input → Preserve-lock → LOOP (max 3-5):
  1. Score text quality (readability, voice, engagement)
  2. Identify flat or robotic sections
  3. If quality target met → EXIT
  4. Rewrite flagged sections with more personality
  5. Restore locked spans
→ Final verification → Output
```

Target the weakest areas. Below ~70% confidence on scores, stop iterating.

## Back-Translation Pipeline

Translation through multiple languages forces structural rebuilding:

```
EN → Chinese (temp 1.3) → Japanese (temp 1.3 + history) → Finnish (Google) → EN (Niutrans)
```

Different language families force different grammatical structures. Different engines prevent pattern inheritance. 4 steps max.

## Model Voice Strip

The "helpful assistant" register is a common pattern in machine-generated text. Strip these:
- Balanced tradeoff offering → pick a side
- Pedagogical scaffolding → cut, trust the reader
- Acknowledgment-prefix ("That's a great question, and...") → cut entirely
- Closing summary recapping → cut
- Symmetric framing of asymmetric tradeoffs → state the asymmetry
- "Important caveats" appended to every claim → keep only material ones
- Hedged conclusions ("I hope this helps") → delete
