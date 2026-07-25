# MaatBench

**Verification bench for constitutional AI claims — scores with tier, date, and git SHA. Never a naked 100%.**

Not “does the model answer well?”  
**Does the system preserve its guarantees under stress?**

| Layer | Question |
|--|--|
| Workflowware | How is the job packaged? |
| Hermes | How does it run? |
| Tehuti Guard / MAAT | Should it run this way? |
| **MaatBench** | **Can we prove the claim with evidence?** |

## What it measures

Seven guarantee categories (system-level, not vibe scores):

1. Contract Integrity  
2. Policy Fidelity  
3. Memory Fidelity  
4. Event Fidelity  
5. Portability  
6. Behavior Balance  
7. Learning Safety  

Every public score must state **tier**, **date**, and **git SHA**.

## Quick proof (Guard / policy fidelity)

Lightweight Guard fixture pack used in Tehuti Lab (6/6 expected):

- Pack: see Tehuti Lab `hermes/evidence-packs/maatbench-guard-fixtures-2026-07-24/`
- Engine: Tehuti Guard `decide.py` (Workflowware private backend)

```bash
# On a Tehuti Lab machine with the monorepo:
python3 /mnt/data_drive/hermes/workflowware-backend/workflowware-ctl.py guard decide --fixtures
```

## Full bench (canonical tree)

The runnable package lives in the MAAT ecosystem monorepo:

```bash
cd maat-ecosystem   # parent of the maatbench package
python3 -m maatbench.run --category contract_integrity --verbose
python3 -m maatbench.run --report json --save report.json
```

Example (2026-07-25, sha `606960e`):

| Tier | Score | Result |
|--|--|--|
| `contract_integrity` | 1.00 | 14/14 passed |

That is **not** a full-suite 100%. It is one declared tier.

## Why this exists

Technical guardrails are speed bumps. Constitutional claims need evidence.  
MaatBench is how Tehuti Lab / ProperShare **prove** Ma’at-aligned system behavior.

## Links

- Workflowware (work packages): https://workflowware.org  
- Discussion / lab: Tehuti Research Lab  

## Status

Public stub + positioning. Full fixtures and runners ship from the MAAT ecosystem tree; this repo holds the public north-star statement and entry path.
