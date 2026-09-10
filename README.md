# Muse Spark 1.2 (xhigh) — ProgramBench submission

- **Model:** `muse-spark-1.2-contributor` on Meta's public API (`api.meta.ai`), reasoning effort **xhigh**
- **Scaffold:** mini-SWE-agent v2.4.2 (single-agent), open source
- **Protocol:** `diff_lang` — no-internet + `task_cleanroom` images. The agent sees only the
  compiled binary (source removed, `.git` reset), reimplements from scratch by interacting with
  it, and never has network access (enforced at the container level).
- **Score:** ~0.572 (mean per-instance test pass-rate over the fixed 200, missing/errored = 0;
  the leaderboard recomputes authoritatively from `_stats/score.json`).
- **Inference date:** 20260908

## Reproduce
```bash
# inference (RevEngBench harness)
revenge mini-batch infer --split task \
  -c reveng/configs/mini/infer/infer_no_int_no_dep.yaml \
  -c reveng/configs/mini/models/muse-spark-1.2.yaml -w 12
# evaluation
revenge eval-cloud submit output/<run> --split task --has-test-branch --force
```

Each test is run up to 3× (pytest-rerunfailures); only the final attempt is scored (flakiness defense).
