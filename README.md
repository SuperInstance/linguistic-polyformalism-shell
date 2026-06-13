# linguistic-polyformalism-shell

An MCP (Model Context Protocol) server that exposes polyformalism thinking as tools for any MCP-compatible AI. Implements five creative-thinking techniques (modeled on brain network dynamics), seven linguistic constraint frames (each derived from a natural language's grammar), insight scoring, and multi-round adversarial debate protocols. Works with Claude Desktop, OpenClaw, Cursor, and Windsurf.

## Why It Matters

LLMs converge on average ideas. The same prompt across different models produces similar answers because they share training-data biases. Polyformalism breaks this convergence by forcing the model through structured cognitive constraints that activate different "thinking modes" — analogous to switching between the brain's Default Mode Network (generative, creative) and Executive Control Network (evaluative, critical).

The linguistic dimension is unique: by constraining the model to "think in" Ancient Greek (categorical/telogical), Classical Chinese (relational/process), or Navajo (shape-and-motion), it produces solutions that English-thinking structurally cannot express. The intersection of multiple linguistic solutions reveals insights invisible to any single language framework.

This is not translation — it is **cognitive restructuring** through grammar.

## How It Works

### Brain Network Analogy

Each technique maps to a brain-network configuration:

| Technique | Brain Analog | α (Novelty Weight) | When to Use |
|-----------|--------------|--------------------:|-------------|
| Ignorant-but-Brilliant | DMN-only (hypofrontality) | 0.8 | Stuck, need fresh perspective |
| Socratic Teacher | Salience → ECN | 0.5 | Too many weak ideas |
| Devil's Advocate | ECN conflict monitoring | 0.3 | One dominant idea, no alternatives |
| Reverse Actualization | BVS reward recoding | 0.5 | Clear goal, unclear path |
| Inject Contrarian | Salience intervention | 0.7 | Converging too fast, groupthink |

The α parameter controls the novelty-adequacy tradeoff in insight scoring:

```
Score = α · Novelty + (1 - α) · Adequacy
```

High α (0.8) biases toward creative, unproven ideas. Low α (0.3) biases toward correct, conventional ideas.

### Linguistic Modes

Seven languages are modeled, each providing orthogonal cognitive constraints:

| Language | Family | Constraint Type | Thinking Style |
|----------|--------|-----------------|----------------|
| Ancient Greek | Indo-European | Boundary | Categorical, telos-driven |
| Classical Chinese | Sinitic | Pattern | Relational, process-oriented |
| Navajo | Athabaskan | Process-Shape | Shape + motion verbs |
| Quechua | Quechuan | Knowledge-Source | Evidentiality markers |
| Korean | Koreanic | Social-Structure | 7 honorific levels |
| Arabic | Semitic | Deep-Structure | Root-and-pattern morphology |
| Finnish | Uralic | Instrument | 15 cases, no gender |

Two languages are **orthogonal** when their constraint types don't overlap — combining them yields maximal cognitive diversity.

### Insight Scoring

```
Score(novelty, adequacy, α) = α · novelty + (1 - α) · adequacy
```

| Score | Quality |
|-------|---------|
| ≥ 4.0 | Exceptional |
| 3.0–3.9 | Strong |
| 2.0–2.9 | Moderate |
| < 2.0 | Weak |

- **Novelty** ∈ [0, 5]: 0 = restatement, 5 = redefines the problem
- **Adequacy** ∈ [0, 5]: 0 = wrong, 5 = correct + elegant + generalizable

### Debate Protocol

Multi-round debates alternate between DMN (generative) and ECN (evaluative) phases:

```
Round k:
  Phase A: Generate (DMN) — 2 generators produce novel perspectives
  Phase B: Evaluate (ECN) — 1 evaluator critiques and scores
  
Synthesis: Cross-reference surviving ideas for emergent insights
```

Stopping criterion: pairwise agreement > 0.7 OR insight scores plateau.

### Time Complexity

- Routing: O(1) lookup table
- Generation prompt: O(P) where P = problem string length
- Debate protocol construction: O(R) where R = rounds
- Linguistic experiment generation: O(L · P) where L = number of languages

## Quick Start

```bash
# Install dependencies
pip install mcp anthropic httpx

# Run as stdio server (default, for Claude Desktop / OpenClaw)
python server.py

# Run as SSE server (for remote access)
python server.py --transport sse --port 8080
```

### MCP Client Configuration

Add to your MCP client config (e.g., `claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "polyformalism": {
      "command": "python",
      "args": ["/path/to/mcp/server.py"]
    }
  }
}
```

## API (MCP Tools)

| Tool | Parameters | Description |
|------|------------|-------------|
| `polyformalism_route` | `problem`, `current_state` | Route to appropriate technique |
| `polyformalism_generate` | `problem`, `technique`, `num_ideas` | Generate in DMN mode |
| `polyformalism_evaluate` | `idea`, `constraints` | Evaluate in ECN mode |
| `polyformalism_score` | `novelty`, `adequacy`, `alpha` | Score insight quality |
| `polyformalism_debate` | `topic`, `rounds`, `models` | Full multi-round debate |
| `polyformalism_linguistic` | `problem`, `languages` | Apply linguistic polyformalism |

## Architecture Notes

Polyformalism is a **meta-γ**: it generates multiple cognitive transforms (**γ₁, γ₂, ..., γₙ**) and applies each to the same problem (**η**), producing a diverse solution set (**C₁, C₂, ..., Cₙ**). The synthesis step finds insights that emerge only from the intersection — the whole is greater than any part. The γ + η = C principle scales recursively: each linguistic frame is itself a γ that restructures η into a different C. The debate protocol is a γ-oscillator: it alternates between generative and evaluative transforms to explore the solution space systematically rather than greedily.

## References

- **DMN/ECN switching**: Beaty, R. E., et al. "Brain networks underlying novel metaphor production." *Brain and Cognition* 111 (2017): 163–170.
- **Linguistic relativity (Sapir-Whorf)**: Boroditsky, L. "How Language Shapes Thought." *Scientific American* 304.2 (2011): 62–65.
- **Adversarial debate in AI**: Irving, G., et al. "AI safety via debate." *arXiv:1805.00899*, 2018.
- **MCP specification**: Anthropic. "Model Context Protocol." *modelcontextprotocol.io*, 2024.
- **Hypofrontality and creativity**: Chávez-Eakle, R. A., et al. "Cerebral blood flow associated with creative performance." *Cortex* 43.5 (2007): 695–705.

## License

MIT
