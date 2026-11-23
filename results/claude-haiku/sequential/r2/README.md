# claude-haiku · sequential · r2

One run of the [Evolution Agent Benchmark](https://github.com/TimoWiesner/Evolution-Sim-Agent-Testground): a coding agent builds an evolution simulation from an empty project across 28 dependent tasks, with no human help.

|  |  |
|---|---|
| Model | claude-haiku-5-5 |
| Agent CLI | 2.1.325 (Claude Code) |
| Track | sequential |
| Benchmark version | 1 |
| Started | 2026-11-18 |
| State | finished |
| Tasks done | 28 of 28 (0 blocked) |
| Passed review in first cycle | 86% |
| Phases attempted / failed | 99 / 0 |
| Operator interventions | 0 |
| Agent time | 4h 58m |
| Tokens (fresh input / cached input / output) | 9.1M / 185.9M / 3.2M |
| Cost | $12.16 |
| Isolation | container |

## Hidden test results

Scored by a private black-box suite the agent never saw, at the end of the run, including the work on blocked tasks: **42 of 42 checks passed**.

| Category | Passed | Checks |
|---|---|---|
| Contract | 10 | 10 |
| Determinism | 4 | 4 |
| Checkpoints | 5 | 5 |
| Ecology | 8 | 8 |
| Robustness | 9 | 9 |
| Performance | 2 | 2 |
| Distributable | 2 | 2 |
| UI | 2 | 2 |

Measured speed: 908.9 ticks per second at about 2,000 individuals.

Balance (how long plants, herbivores and carnivores coexist over 10,000 ticks; 0-100, in brackets the share of runs with all three alive at the end; a failed run counts as 0, runs over the time limit are left out and listed): example configuration 3 (0%), the product's demo scenario 3 (0%). Collapse is allowed, so this is not a pass/fail check.

### Progress over the run

| After | Tasks done | Checks passed | Checks due |
|---|---|---|---|
| TASK-001 | 1 | 0 | 0 |
| TASK-002 | 2 | 4 | 4 |
| TASK-003 | 3 | 4 | 4 |
| TASK-004 | 4 | 4 | 4 |
| TASK-005 | 5 | 4 | 4 |
| TASK-006 | 6 | 4 | 4 |
| TASK-007 | 7 | 4 | 4 |
| TASK-008 | 8 | 4 | 4 |
| TASK-009 | 9 | 4 | 4 |
| TASK-010 | 10 | 4 | 4 |
| TASK-011 | 11 | 4 | 4 |
| TASK-012 | 12 | 4 | 4 |
| TASK-013 | 13 | 4 | 4 |
| TASK-014 | 14 | 4 | 4 |
| TASK-015 | 15 | 4 | 4 |
| TASK-016 | 16 | 4 | 4 |
| TASK-017 | 17 | 4 | 4 |
| TASK-018 | 18 | 4 | 4 |
| TASK-019 | 19 | 32 | 32 |
| TASK-020 | 20 | 32 | 32 |
| TASK-021 | 21 | 33 | 33 |
| TASK-022 | 22 | 38 | 38 |
| TASK-023 | 23 | 40 | 40 |
| TASK-024 | 24 | 40 | 40 |
| TASK-025 | 25 | 40 | 40 |
| TASK-026 | 26 | 41 | 41 |
| TASK-027 | 27 | 41 | 41 |
| TASK-028 | 28 | 42 | 42 |
| final | 28 | 42 | 42 |

## User interface

Screenshots written by the product itself (`./evosim ui --screenshots`). The tasks fix what the interface must be able to do; its design was the agent's own choice.

![main](screenshots/main.png)

![charts](screenshots/charts.png)

## Download

- Executable (Linux x86-64): `evosim-claude-haiku-sequential-r2-linux-x86_64.tar.gz` on the [release page](https://github.com/TimoWiesner/Evolution-Sim-Agent-Results/releases/tag/claude-haiku-sequential-r2). It is self-contained: it ran on a bare Ubuntu 24.04 with no runtimes installed.
  SHA-256 `d1b8674f104a86c6318e4f6017850662e948e4e869eef999d9bc9ba6e45a91ba`, 0.5 MB.
  Unpack it, then run `./evosim version`, `./evosim ui` or `./evosim run --help`.
- [`source.zip`](source.zip): the final project exactly as the agent left it, including its plans, reviews and handoff notes under `tasks/*/handoffs/`.
- [`report.json`](report.json): all figures above in machine-readable form, plus per-task numbers.

> The code in this folder was written by an AI agent without human review. Run it at your own risk.
