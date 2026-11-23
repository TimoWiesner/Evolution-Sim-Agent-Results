# Benchmark version 1: analysis

Written by hand on 2026-11-23; the generated [README](README.md) has every figure in full.

Seven runs of benchmark version 1, all on the sequential track: three Claude models through Claude Code and four GPT models through the Codex CLI. Every agent got the same 28 dependent tasks, starter project and black-box test suite (42 checks, suite version 6). Each model ran once, so the figures below describe one run, not a model's average.

Not included:
- A Claude Fable run that was stopped early and deleted.
- An earlier Claude Haiku run (`r1`) made with a pre-release task set (27 tasks, suite version 3).
- The `gpt-astra` run in benchmark version 2, which is still in progress.

## Comparison

| Model | Tasks done | Hidden checks | Review passed in 1st cycle | Agent time | Output tokens | Cost | Ticks/s | Balance (example / demo) |
|---|---|---|---|---|---|---|---|---|
| claude-opus-5-5 | 28/28 | **42/42** | **100%** | 6h 15m | 1.6M | $100.73 | 378 | **72 / 100** |
| claude-sonnet-5-5 | 28/28 | **42/42** | 93% | 3h 42m | 971k | $30.76 | 339 | 25 / 29 |
| claude-haiku-5-5 | 28/28 | **42/42** | 86% | 4h 58m | 3.2M | $12.16 | **909** | 3 / 3 |
| gpt-6.1-terra | 28/28 | **42/42** | 93% | **2h 14m** | **307k** | — | 319 | 7 / 6 |
| gpt-6.1-sol | 28/28 | 41/42 | **100%** | 6h 44m | 921k | — | 176 | 4 / 12 |
| gpt-6-luna | 28/28 | 39/42 | 79% | 6h 01m | 797k | — | 39 | 2 / 12 |
| gpt-6-astra | 1/28 | 4/42 | — (TASK-002 never passed) | 35m | 75k | — | — | — |

- **Cost** is what the CLI reports. Codex reports no cost, so the GPT runs show "—", which does not mean zero.
- **Agent time** is the time spent in agent calls. Waiting for provider usage limits is left out.
- **Balance** runs from 0 to 100 and measures how long plants, herbivores and carnivores coexist over 10,000 ticks.

## Main differences

**1. Most models built a working product, so passing the checks does not separate them much.**
- Six of seven runs finished all 28 tasks, and four passed every hidden check: Opus, Sonnet, Haiku and Terra.
- Sol missed one check, X02: the built `dist/evosim` gives a different `state_hash` than `./evosim`, so the shipped binary does not reproduce the development build exactly.
- Luna missed three:
  - C10: `batch` refuses an output directory that does not exist yet.
  - E06: well-fed herbivores never reproduced.
  - P02: 39 ticks per second, below the required 100.

**2. The ecosystem is where the models really differ, and only Opus got it working.**
- Opus is the only model whose plants, herbivores and carnivores survive together:
  - In its own demo scenario all three survive the full 10,000 ticks in all 6 runs (score 100).
  - With default parameters they survive in half of the runs (score 72).
- Every other product collapses: the first kind dies out after a median of 200 to 3,000 ticks.
  - Sonnet comes closest (25 / 29).
  - Haiku, Terra, Sol and Luna score 12 or less.
- Terra and Sol keep their populations tiny, with a mean of 36 to 136 individuals. That passes the checks, but the worlds are close to empty.
- Every run had the same balance task (TASK-027), with the same time and the same rules against forcing survival.

**3. gpt-6-astra failed because it read one requirement literally, not because of its code.**
- TASK-002 required that "`./evosim version` prints the contract JSON after `./setup.sh` in a fresh container".
- Astra's reviewer insisted on starting a real new container inside the agent's sandbox. The sandbox does not allow that ("Operation not permitted"), so the reviewer failed the task in all three review cycles.
- The code itself worked: the project skeleton, tests and build were fine.
- The run was given a fourth cycle by operator intervention (`unblock`, shown in the results). Astra again declared the requirement "environmentally blocked" and did not try a clean checkout instead.
- Because every later task depends on TASK-002, 26 tasks never started.
- Every other model, from both vendors, read the same sentence as "works from a clean setup" and passed it in the first cycle.
- This result stands for version 1. Benchmark version 2 changes only this wording, in TASK-002 and in the contract, and Astra is being run again under it.

**4. Speed and price do not follow quality.**
- **Terra** was the fastest and leanest full run, with every check passed: 2h 14m and 307k output tokens, about a fifth of what Opus used.
- **Haiku** was the cheapest Claude run at $12.16. It used the most tokens of all (198M, almost all cached input) and needed a second review cycle on four tasks. Its product was the fastest, at 909 ticks per second.
- **Opus** cost $100.73, about three times Sonnet and eight times Haiku. It is also the only run with a working ecosystem.
- **Luna** and **Sol** took about as long as Opus. Luna's product came out the weakest of the finished runs.

**5. How strict each model was as its own reviewer.**
- Opus and Sol passed every task in the first review cycle.
- Luna needed a second cycle on six tasks and still had the most failed hidden checks. Its reviews found problems, but not the ones the hidden suite tests.
- Astra shows the opposite failure: a reviewer so literal that it blocked working code.

## How far the runs are comparable

- **Same versions:** all seven runs use benchmark version 1 and suite version 6, and each final state was scored after the run.
- **Different harness commits:** the runs did not all start from the same harness commit. As far as the agents can see, these differences remain:
  - Sonnet and Haiku (`b0ff236`) did not yet have the contract sentence stating the 300 s / 900 s time limits for the balance runs. The time limits themselves were the same for everyone.
  - Luna, Terra and Sol found the phase skills under `.agents/skills/`, Opus and Astra under `.bench/skills/`. The text was the same, and every agent read the files through the path given in its prompt.
  - Terra's harness had one uncommitted change: its profile was switched to `gpt-6.1-terra` before the start.
- **Not counted:** waiting for provider usage limits and calls repeated after outages are not counted. They cost real time (Opus about 19 h of waiting, Sol about 12 h), but that time is not part of agent time.
- **One run each:** there is one run per model, on one machine, with Claude Code 2.1.325 / 2.1.328 and codex-cli 0.164.0. Small differences, for example in agent time, should not be over-read.
