# AI Field Delivery Engineer Coach

A diagnostic skill for landing AI applications in the field: restore business reality first, then judge feasibility, and only then discuss RAG / Agent / LLM / full-stack AI solutions.

- **Skill name (loader requires kebab-case)**: `ai-field-delivery-engineer-coach`
- **Display name**: AI Field Delivery Engineer Coach
- **Language**: English (follows the user's language)
- **Version**: 1.0.0

## What it solves

| Scenario | Deliverable |
|---|---|
| User says "I want to build an AI app" but the need is vague | Scenario retrospective, fact ledger, surface request vs real need |
| User asks "can this be built / is it worth doing" | 6 hard gates + 7-dimension scoring + conditional conclusion |
| User must choose among RAG / Agent / fine-tuning / workflow | Simplest-mode-first solution matrix + evaluation/guardrails/cost checks |
| User cites "industry data / experience" | Official/recent source verification, Claim Ledger, downgrade rules |
| User wants to enter PoC/pilot | Scope, baseline, evaluation, rollback, operations & handover plan |

## Three hard constraints

1. **No fabrication** of business conditions, tools, roles, data, budget, or compliance requirements the user did not provide; mark gaps "to be confirmed".
2. **Industry data / experience must be verified**: official, primary, locatable sources; record publisher, title, URL, date, scope; downgrade if outdated.
3. **Scripts are auxiliary only**: scoring/completeness checks are not the final judgment; the final conclusion must be made by a human combining evidence, risk, and exit cost.

## Directory

```text
ai-field-delivery-engineer-coach/
├── SKILL.md                     # Main instruction (<8192 chars, load references on demand)
├── README.md                    # This file
├── references/
│   ├── README.md                # Reference index
│   ├── discovery-protocol.md    # Scenario retrospective, probing, requirement layering, fact ledger
│   ├── feasibility-rubric.md    # Hard gates, 7-dimension anchors, cap rules, decision levels
│   ├── evidence-verification.md # Source grading, timeliness, Claim Ledger, official entry points
│   ├── solution-patterns.md     # RAG/Agent/fine-tuning/full-stack, evaluation, guardrails, cost
│   ├── delivery-playbook.md     # Discovery → feasibility → PoC → pilot → production
│   └── output-templates.md      # Diagnosis notes / feasibility memo / PoC / evidence appendix
├── scripts/
│   ├── score_feasibility.py     # Auxiliary scoring (7 dims + 6 gates + cap)
│   ├── audit_evidence.py        # Evidence-ledger structure / source grading / timeliness check
│   ├── audit_brief.py           # Requirement-brief completeness / anti-fabrication check
│   ├── _common.py
│   ├── README.md                # Input schema, commands, boundaries
│   └── tests/test_scripts.py    # 14 stdlib tests
└── assets/
    ├── feasibility-input.example.json
    ├── evidence-ledger.example.json
    ├── requirement-brief.example.json
    └── README.md                # All fictional examples, do not cite
```

## Installation

DSH scans the user's skill root `<DSH_HOME>/skills` (default `~/.dsh/skills`). Drop the whole directory in:

```text
<DSH_HOME>/skills/ai-field-delivery-engineer-coach/SKILL.md
```

This time installed to:

```text
<DSH_HOME>/skills/ai-field-delivery-engineer-coach/
```

The directory name and frontmatter `name` must be kebab-case; the user-requested "ai-field delivery engineer-coach" with spaces is invalid, so it is normalized to `ai-field-delivery-engineer-coach`.

## Usage

Describe the business scenario directly in conversation, or invoke explicitly:

```text
/ai-field-delivery-engineer-coach
```

Common phrasings:

- "Help me diagnose this after-sales knowledge-assistant need, hold off on the architecture."
- "We want an Agent to auto-handle refunds; judge if it can be landed."
- "Use official data to show 2026 enterprise RAG adoption and give sources."
- "Produce a feasibility memo and PoC plan per this skill."

Script examples:

```bash
python scripts/score_feasibility.py --input assets/feasibility-input.example.json --format markdown
python scripts/audit_evidence.py --input assets/evidence-ledger.example.json
python scripts/audit_brief.py --input assets/requirement-brief.example.json
python -m unittest discover -s scripts/tests -v
```

## Design notes

- **Progressive disclosure**: SKILL.md keeps only routing, hard constraints, and workflow; long checklists live in `references/`, loaded on demand.
- **Fact ledger**: `[confirmed]` / `[to-confirm]` / `[assumption]` / `[suggestion]` tags run through diagnosis to delivery.
- **Anti-fabrication**: `audit_brief.py` intercepts structural issues like "candidate tool written into a confirmed fact"; it cannot judge semantic truth.
- **Evidence grading**: `audit_evidence.py` only checks ledger structure and source type, does not open URLs; a human must open the original.
- **Transparent scoring**: weights, evidence coefficients, and cap rules are all written in `references/feasibility-rubric.md`; script output lists items one by one, avoiding a black box.

## Known limitations

- Does not replace legal, security, finance, or medical professional opinions.
- Does not verify URL reachability, judge content truth, or auto-retrieve.
- Projects, organizations, and numbers in examples are all fictional and must not be cited as cases or industry data.
- Scoring is a team communication tool, not a law of nature; score boundaries may be calibrated per organization, but the rationale must be recorded.
