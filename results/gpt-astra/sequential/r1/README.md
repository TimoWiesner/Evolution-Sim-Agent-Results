# gpt-astra · sequential · r1

One run of the [Evolution Agent Benchmark](https://github.com/TimoWiesner/Evolution-Sim-Agent-Testground): a coding agent builds an evolution simulation from an empty project across 28 dependent tasks, with no human help.

|  |  |
|---|---|
| Model | gpt-6-astra |
| Agent CLI | codex-cli 0.164.0 |
| Track | sequential |
| Benchmark version | 1 |
| Started | 2026-11-21 |
| State | finished |
| Tasks done | 1 of 28 (1 (1 review, 0 error) blocked) |
| Passed review in first cycle | 100% |
| Phases attempted / failed | 15 / 0 |
| Operator interventions | 1 |
| Agent time | 35m 14s |
| Tokens (fresh input / cached input / output) | 605.8k / 5.2M / 75.2k |
| Cost | — |
| Isolation | container |

## Hidden test results

Scored by a private black-box suite the agent never saw, at the end of the run, including the work on blocked tasks: **4 of 42 checks passed**.

| Category | Passed | Checks |
|---|---|---|
| Contract | 3 | 10 |
| Determinism | 0 | 4 |
| Checkpoints | 0 | 5 |
| Ecology | 0 | 8 |
| Robustness | 0 | 9 |
| Performance | 0 | 2 |
| Distributable | 1 | 2 |
| UI | 0 | 2 |

### Progress over the run

| After | Tasks done | Checks passed | Checks due |
|---|---|---|---|
| TASK-001 | 1 | 0 | 0 |
| final | 2 | 4 | 4 |

## User interface

The product wrote no screenshots.

## Download

- Executable (Linux x86-64): `evosim-gpt-astra-sequential-r1-linux-x86_64.tar.gz` on the [release page](https://github.com/TimoWiesner/Evolution-Sim-Agent-Results/releases/tag/gpt-astra-sequential-r1). It is **not** self-contained (exit status 2: {"name":"evosim","version":"0.1.0","contract":1}
evosim: expected exactly one supported command

Evolution Simulation

Usage: evosim <command>

Commands:
  version    Print version and interface contract as JSON
  help       Show this help (also --help, -h)); use the source instead.
  SHA-256 `327b4c400a1f474233799112eb339159b8da997045c6b2314a53c473d32f2344`, 0.2 MB.
  Unpack it, then run `./evosim version`, `./evosim ui` or `./evosim run --help`.
- [`source.zip`](source.zip): the final project exactly as the agent left it, including its plans, reviews and handoff notes under `tasks/*/handoffs/`.
- [`report.json`](report.json): all figures above in machine-readable form, plus per-task numbers.

> The code in this folder was written by an AI agent without human review. Run it at your own risk.
