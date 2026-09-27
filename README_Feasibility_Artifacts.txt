# Stage 2 report-only feasibility artifacts

This archive accompanies the revised manuscript by Doğu Sırt. It contains an executed engineering demonstration, its frozen source changes, and a separate prospective human-study record specification.

## What was executed

- A synthetic, package-free C#/.NET 8 baseline, commit `8858837c4dad57fb3b2083d1f5e9afcb88d3e1f2`.
- Twenty-four independent agent sessions, eight for each of three tasks. All first final submissions were retained. These are local pull-request-equivalent commits, not hosted pull requests.
- Six report-only checks, three head repetitions at each concurrency of 1, 2, and 4, and one common-parent scan per scenario. There are 216 head pipeline repetitions, 3 parent repetitions, and 1,314 planned gate attempts.
- Public compile/regression checks outside the timed replay. These are not hidden task-acceptance scores.

Read `measurement_summary/summary.md` for actual execution status, timing, and limits. The final CSV is complete. The append-only JSONL journal lacks 14 entries, as documented in `records/EVIDENCE_INTEGRITY_NOTE.md`. The original journal is retained unchanged, and analyses use the CSV plus hash-checked per-attempt results. No fabricated or synthetic runtime rows are included in `measurements/`. Instrument fixtures are isolated in `instrument_validation/` and analyzer unit-test files.

Retrospective external task checks were added after generation and gate measurement. Read `post_generation_validation/combined_summary.json` and the per-task documentation. All 24 retained heads passed the selected checks in the final campaigns, with 376 candidate/check observations across task-specific suites. This count is not 376 independent changes. T1 includes 23 behavioral and three architectural checks per change. T2 includes nine behavioral cases. T3 includes ten common cases and two separate conditional-update probes. Baseline controls and unsupported interfaces are reported separately. Earlier T2 evaluation attempts are retained with the documented constructor-binding correction. No candidate was repaired in response to these checks.

## Evidence map

| Path | Contents |
|---|---|
| `baseline/` | Readable immutable starting repository and task prompts |
| `benchmark.bundle` | Git repository objects and all run branches |
| `traces/` | Exact prompts, terminal command/output records, timing logs, summaries, and base-to-head diffs |
| `records/` | Local prespecified design, original manifests, corpus counts, manuscript result text/tables, scope erratum |
| `preflight/` | Actual per-head restore/build/public-test logs and statuses |
| `gate_analyzer/` | Custom C# checks, metric definitions, source hashes, fixture results |
| `experiment_tools/` | SAST wrapper, timing runner, aggregation, and replay scripts |
| `measurements/` | Raw command outcomes, per-gate timing, findings, host details, pinned commands, logs and hashes |
| `measurement_summary/` | Derived tables and paired baseline/head alert summaries |
| `protocol_supplement/` | Prospective human-study templates, not observations |
| `post_generation_validation/` | Retrospective external task checks, frozen harnesses, execution logs, observed outcomes, and replay instructions |
| `analysis_provenance/` | Original integrity audit, line-count, and manuscript table-generation scripts |
| `records/adjudication_packet_unrated.csv` | All 144 change/gate pairs with blank human-label fields |

## Reproduce the retained-change replay

Use Linux, Git, Python 3.12 or later, and the official .NET SDK 8.0.425. The SDK is not redistributed here. The source repository needs no external NuGet packages. The timing runner uses Linux `wait4` accounting. Choose a new output directory.

```bash
python experiment_tools/reproduce.py --archive-root /absolute/path/Feasibility_Artifacts --dotnet /absolute/path/to/dotnet --output /absolute/path/to/new-replay
```

The script reconstructs the recorded baseline and all 24 head worktrees from the bundle, restores the package-free projects, repeats the public preflight outside timing, builds the analyzer, generates commands for the new paths, and executes the same 1/2/4 scenario order. It creates new measurements without overwriting the original evidence. Exact runtime values are not expected to reproduce across hosts. `records/experiment_manifest.json` and raw measurement commands retain the original workspace paths as provenance. The replay script replaces execution paths as needed.

Recompute the manuscript result paragraphs and tables with `python analysis_provenance/write_empirical_results.py --work-root /absolute/path/Feasibility_Artifacts`. The other provenance scripts preserve the original workspace audit procedure and expect reconstructed source workspaces. Portable raw timing summaries use `experiment_tools/aggregate_measurements.py`.

The later task checks have their own replay commands and output locations. See `post_generation_validation/T1/README.md`, `post_generation_validation/T2/README.md`, and `post_generation_validation/T3/REPLAY.md`. Recompute their combined descriptive counts with `python analysis_provenance/summarize_post_validation.py --root /absolute/path/Feasibility_Artifacts/post_generation_validation`. Do not merge their execution durations into the original gate timing experiment.

To inspect one change:

```bash
git clone benchmark.bundle inspection
git -C inspection diff 8858837c4dad57fb3b2083d1f5e9afcb88d3e1f2 <head-commit-from-manifest>
```

## Interpretation and known limits

The baseline contains 17,914 physical C# lines, of which 1,895 are implementation and 16,019 are tests. It is a small application with generated regression fixtures, not a representative 18,000-line production system. The README wording about a hidden harness is corrected in `records/FEASIBILITY_SCOPE_NOTES.md`. No executable acceptance oracle was frozen before agent generation. Later external task checks are supplied separately under `post_generation_validation/`. Their evaluators had access to candidate source. They are retrospective and unblinded, not preregistered validation or human adjudication. Their observations do not alter the original gate timing results. No branch-coverage or mutation score is reported.

Complexity and duplication use custom stated syntax/token definitions, not SonarQube-equivalent values. The timed architectural gate inspects project-reference XML and explicit namespace syntax. Two compiled assembly-reference checks run in the separate public suite. Dependency findings request policy review and are not vulnerability determinations. Size counts whole changes, unlike the framework's provisional per-step limit. SAST uses the SDK's Security analyzers and does not establish complete security coverage.

All tool warnings and threshold exceedances are unadjudicated. Human-label fields intentionally remain empty. No independent human false-positive, missed-defect, reviewer-time, Study A/B, longitudinal, full-CAI, or general-scalability result exists in this archive. The local design was fixed in advance but was not publicly preregistered. Thresholds were not calibrated from human repository history.

Generation used the ChatGPT Codex agent service, which did not expose an immutable backend model version or sampling configuration. Retained prompts, source, and traces support source replay but not guaranteed regeneration. Recorded terminal traces contain commands and outputs, not private internal reasoning. No Stage 2 feedback was given to generation sessions.

Scenarios ran in fixed order without operating-system cache flushing. Queue delay is batch wait per three-repetition job. Reported per-repetition gate sums exclude queueing and inter-gate logging overhead. Full-job timings are retained. Throughput includes scheduled parent work in its denominator. CPU and RSS have the documented `wait4` accounting limits, and RSS is not an aggregate concurrent process-tree peak. Repetitions are technical repetitions of 24 changes, not 216 independent agent samples.

`SHA256SUMS.txt` covers every other file in this archive. Verify it from this directory with `sha256sum -c SHA256SUMS.txt`.
