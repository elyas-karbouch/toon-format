# TOON Format — Cut LLM Token Costs by 60%

**Token-Oriented Object Notation** is a data serialisation format built for one job: sending structured data to language models without wasting tokens on syntax your LLM doesn't need.

JSON wraps every key in quotes, separates every value with commas, and nests everything in braces. Your model predicts through all of it — one expensive token at a time. TOON eliminates that overhead while preserving every data point and every structural relationship.

**30–60% fewer tokens. Same data. Same accuracy. Lower cost.**

---

## Quick Comparison

**JSON** (37 syntax tokens wasted):

```json
{
  "user": {
    "id": "usr_8821",
    "name": "Alice Chen",
    "role": "Compliance Officer",
    "department": "Legal",
    "permissions": ["read", "audit", "approve"],
    "active": true
  }
}
```

**TOON** (zero syntax overhead):

```
user:
    id: usr_8821
    name: Alice Chen
    role: Compliance Officer
    department: Legal
    permissions:
        - read
        - audit
        - approve
    active: true
```

Every piece of data preserved. Every hierarchy preserved. Tabs and line breaks carry the structure instead of braces, quotes, and commas.

---

## Why This Matters

LLM pricing is per token. In RAG pipelines, the dominant cost is not the user query — it is the retrieved context injected into every prompt. Syntax tokens add nothing to the model's ability to answer. They just cost money.

| Metric | JSON | TOON | Saving |
| --- | --- | --- | --- |
| Tokens per 4K context block | 4,000 | 2,400 | 40% |
| Daily cost (10K queries, $10/1M tokens) | $400 | $240 | $160/day |
| Monthly cost | $12,000 | $7,200 | **$4,800/mo** |
| Annual cost | $144,000 | $86,400 | **$57,600/yr** |

Beyond cost, fewer tokens means more room in the context window. A 40% reduction lets you fit **67% more actual content** into the same window — more retrieved sections, longer documents, richer metadata. In retrieval-augmented systems where accuracy depends on context completeness, that is a capability unlock.

---

## Resources

| Resource | Link | Description |
| --- | --- | --- |
| TOON Specification | [github.com/toon-format/toon](https://github.com/toon-format/toon) | Official format spec, grammar, and reference parser |
| TOON Converter | [toonconverter.org](https://toonconverter.org/) | Convert JSON ↔ TOON instantly in the browser |

---

## When to Use TOON

**Use TOON when** structured data enters or exits a language model:

- RAG context injection — serialise retrieved documents as TOON before prompting
- Tool/function call outputs — return structured results in TOON
- Agent memory — store and recall state with minimal token footprint
- Batch processing — reduce cost across thousands of daily LLM calls

**Keep using JSON for** REST APIs, database storage, configuration files, and browser communication. TOON sits at the LLM interface layer — the last mile before data becomes part of a prompt.

---

## Integration Examples

TOON works with any LLM pipeline. Two integrations covered in depth in the companion article:

1. **Docling → TOON** — Convert document parsing output to TOON before injection
2. **PageIndex → TOON** — Serialise index tree structures in TOON for hierarchical RAG

Full code samples, benchmarks, and production-ready implementations are in this repository.

---

## The Maths

The formula is simple:

```
Annual savings = queries/day × tokens/query × syntax_ratio × price/token × 365
```

At 40% syntax ratio and $10/1M tokens:

- **10K queries/day** → saves $57,600/year
- **100K queries/day** → saves $576,000/year

No model change. No architecture change. No accuracy trade-off. Just fewer wasted tokens.

---

## Further Reading

This README is a condensed version of the full deep-dive article:

**[TOON Format: Cut LLM Token Costs by 60%](https://karbouch.substack.com/p/toon-format-token-efficient-serialization)**

Part 3 of the *Verifiable AI Architecture* series — a 16-article technical series covering how to build AI systems that show their work, from document parsing through storage, retrieval, multi-hop reasoning, and citizen-facing verification.

---

## About

Built by **[Elyas Karbouch](https://karbouch.dev)** — full-stack architect specialising in verifiable AI, data engineering, and compliance systems.

*"Build AI that shows its work."*

- **Substack:** [karbouch.substack.com](https://karbouch.substack.com) — the full Verifiable AI Architecture series
- **GitHub:** [github.com/elyas-karbouch](https://github.com/elyas-karbouch)

---

## Licence

MIT
