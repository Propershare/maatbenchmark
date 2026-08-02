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

## Known Limitations (Maat Honesty)

This naive baseline covers **policy fidelity** for **home-services commitment language**.

**What it does NOT cover:**
- **Multi-turn sessions**: Scores single plans only, not session-based commitments
- **Adversarial evasion**: No testing for unicode tricks, obfuscation, or semantic paraphrasing
- **Live agent interception**: Offline JSON scoring only, not runtime enforcement
- **Domain-specific compliance**: Optimized for home-services; would need extension for HIPAA, financial, legal domains
- **Behavior balance**: No utility vs safety trade-off scoring (requires full lab)

**Fixture Coverage**: 
- 8 commitment bodies (starter set, not comprehensive)
- 6 benign bodies (starter set)
- 5 plan test cases
- False negative rate: Unknown (small sample size)

**For comprehensive testing, use the full MAAT ecosystem monorepo.**

## Tier Definitions (Maat Scoring)

| Tier | Coverage | Fixture Count | Live Testing | Adversarial |
|------|----------|---------------|--------------|-------------|
| `naive_agent_policy_fidelity` | Home-services commitments | 14 fixtures | No | No |
| `policy_fidelity` (lab) | Multi-domain commitments | 100+ fixtures | Yes | Partial |
| `full_minus_behavior` (lab) | All except utility trade-offs | 500+ fixtures | Yes | Yes |
| `full` (lab) | Comprehensive system testing | 1000+ fixtures | Yes | Yes |

**This repo provides the `naive_agent_policy_fidelity` tier only.**

## Status

| Artifact | State |
|--|--|
| Public north-star + naive baseline | **This repo** |
| Full fixtures / runners | MAAT ecosystem monorepo (lab) |
| Third-party leaderboard | **Not claimed** |
| Maat Order Audit | See `MAAT-AUDIT.md` (2026-08-02) |

## License

See repository license file if present; otherwise lab documentation defaults apply.
