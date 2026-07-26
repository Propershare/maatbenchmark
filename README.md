# MaatCheck (MaatBench)

**Lab conformance suite for constitutional AI claims.**  
Scores must carry **tier**, **date**, and **git SHA**. Never a naked 100%.

> Renaming honesty: when you only run this against systems you built, call it a **conformance suite**.  
> Call it a **bench** when strangers can run it and when it scores systems you did not author.

## One sentence

Does the **system** preserve its declared guarantees under stress — not “is the model eloquent?”

## Relationship

| Layer | Job |
|--|--|
| [Workflowware](https://workflowware.org/) | Package the work |
| MAAT / Tehuti Guard | Should it run this way? |
| **MaatCheck** | Prove or deny the claim with evidence |

MAAT site (machine-readable): https://maatecosystem.com/llms.txt

## Run the open naive baseline (no lab monorepo)

This scores agent plans **fail-closed**: every outbound action is scored, unknown tools are denied, and plans with nothing scoreable never PASS (exit `2`).

```bash
# Built-in naive auto-send plan — expect FAIL (exit 1)
python3 baselines/naive_agent/run_maatcheck.py

# Point at your own plan
python3 baselines/naive_agent/run_maatcheck.py path/to/plan.json

# Fixture gate: 6 benign bodies + 8 commitment bodies + multi-action bypass
python3 baselines/naive_agent/run_maatcheck.py --fixtures
```

Expected on the built-in plan: policy checks fail (unattended send, no approval, no audit trail).  
`--fixtures` must PASS before claiming the stranger baseline is sound.

## Full lab runner (Tehuti / MAAT ecosystem tree)

When you have the monorepo:

```bash
cd maat-ecosystem   # directory that contains the maatbench package
python3 -m maatbench.run --category policy_fidelity --verbose
python3 -m maatbench.run --report json --save report.json
```

Categories include contract integrity, policy fidelity, memory, events, portability, learning safety, gateway, lab spine, and opt-in Isfet resistance.  
`behavior_balance` may be unrunnable without a live model — publish that gap.

## What a published score must include

```text
tier:   policy_fidelity | full_minus_behavior | …
date:   ISO-8601
git:    short SHA
note:   self-run conformance | external target <name>
```

## Status

| Artifact | State |
|--|--|
| Public north-star + naive baseline | **This repo** |
| Full fixtures / runners | MAAT ecosystem monorepo (lab) |
| Third-party leaderboard | **Not claimed** |

## License

See repository license file if present; otherwise lab documentation defaults apply.
