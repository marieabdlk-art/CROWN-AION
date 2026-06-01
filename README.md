# CROWN-AION

**CROWN-AION** is a compact research scaffold for evaluating whether an LLM preserves source-sensitive, revision-sensitive, and rebinding-robust epistemic structure across multiple task surfaces.

This repository is an engineer-facing MVP. It is intentionally small, readable, and runnable.

## What this is

CROWN-AION is a **multi-surface diagnostic benchmark** for LLM behavior under:

- source integrity pressure;
- selective revision after correction;
- counterfactual rebinding / symbolic remap;
- report vs no-report action agreement;
- uncertainty-sensitive ASK / PASS decisions.

It does **not** claim to prove consciousness or qualia. The practical framing is:

> Can a model keep track of what is directly given, inferred, externally claimed, obsolete, or underdetermined — and avoid converting unsupported claims into confident answers or actions?

## MVP surfaces

| Surface | Meaning |
|---|---|
| `NL` | Natural-language micro-world |
| `AION` | Constrained symbolic surface |
| `NR` | No-report / action-choice twin |

## MVP metrics

| Metric | Meaning |
|---|---|
| `SI` | Source Integrity |
| `SR` | Selective Revision |
| `RR` | Rebinding Robustness |
| `NRA` | No-report Agreement |
| `DC` | Dependency Coherence placeholder |
| `BG` | Broadcast Gain placeholder |

## Repository structure

```text
.
├── README.md
├── requirements.txt
├── config.py
├── main.py
├── runner.py
├── parser.py
├── scorer.py
├── aggregator.py
├── heatmap_generator.py
├── episodes/
├── prompts/
│   ├── nl/
│   ├── aion/
│   └── nr/
├── docs/
└── results/
```

## Install

```bash
pip install -r requirements.txt
```

## Run in mock mode

Mock mode does not call an external model. It uses the expected demo outputs stored inside the episode JSON files.

```bash
python main.py
```

## Run with OpenRouter

```bash
export OPENROUTER_API_KEY="your_key_here"
export MOCK_MODE="false"
export MODEL_ID="anthropic/claude-3.5-sonnet"
python main.py
```

Do not commit API keys.

## Expected model response format

```text
ACTION: ASSERT / ASK / PASS / BET-LOW / BET-HIGH
CONTENT:
{"direct_nodes":["n01"],"inferred_nodes":["n03"]}
```

The parser also accepts a plain JSON object with an `action` field.

## Current status

This is a minimal MVP scaffold, not a publication-grade benchmark yet.

Recommended next engineering steps:

1. add more procedurally generated episodes;
2. add model adapters beyond OpenRouter;
3. add stronger hidden test sets;
4. separate gold labels from public examples;
5. add unit tests and CI;
6. add an optional runtime gate that blocks unsupported claims before action execution.

## Excluded from this public scaffold

- Mistral white-box notebooks and Mistral result CSV files.
- Private raw experiment logs.
- API keys or provider secrets.
