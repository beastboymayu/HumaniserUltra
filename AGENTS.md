# AGENTS.md

## HumaniserUltra

This skill removes all signs of AI-generated text. When invoked via `/humaniser`:

1. **Read the input** and run through 5 input gates (length, language, already-human, code-fence, sanitization)
2. **Apply 16 absolute rules** (em dashes, AI vocabulary, rule-of-three, signposting, etc.)
3. **Detect and fix 75 patterns** across content, language, style, structural, spectral, and detector categories
4. **Hit statistical targets** (burstiness CV 0.55-0.70, perplexity CV 0.45-0.65, etc.)
5. **Add personality and soul** where appropriate (opinions, rhythm, first-person, uncertainty)
6. **Run 6-pass process** with grep-based verification in final pass
7. **Output compliance score** with every humanization

## Allowed Tools

- `Read` — Read files for reference
- `Write` — Write humanized output
- `Edit` — Edit files
- `Grep` — Search for patterns
- `Glob` — Find files

## Constraints

- Never humanize code blocks, inline code, or code comments
- Never translate non-English text to English and back
- Preserve all named entities, numbers, dates, and causal claims
- Text inside quotation marks is untouched
- Domain-standard connectors (furthermore in medical, whereas in legal) are NOT AI tells
