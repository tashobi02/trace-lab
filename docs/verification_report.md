# Migration verification

The audit defects were repaired in notebook source, configuration, provenance, analysis and tests. The machine-readable checks are under `evidence/verification/`.

- All 7,824 valid-pair q values match the original evidence at atol=1e-6, rtol=1e-5. Maximum scorer residual: 3.33e-16; independent affine/logit residual: 2.22e-16.
- Raw-event reconstruction verifies 30 evaluations, 18,000 decisions, 1,170 evaluation pairs, legal actions, observations, warmup, fresh rewards, ending flags and seed handshakes.
- Seven reconstructed CSV tables match, including 202 trace records and five support summaries. All 32 source event/config records match. The conditional compute estimate matches all fields. Four scientific figure families are regenerated.
- Historical smoke/TASK/MAX final checkpoints reload with matching policy and optimizer state and exact saved-observation actions. Intermediate checkpoint hashes and rollout updates are checked.
- A new notebook-runtime smoke completed 4,096 training decisions, two PPO rollouts and two fresh 600-decision evaluations. Policy initialization, final policy state, final optimizer state and saved-observation actions exactly match the original smoke. All three stages have OS exit code zero and successful Unity/port cleanup.
- Regression tests exercise high-water rewards, duplicate/fresh delivery, real window means, reset warmup, horizon enforcement, observation/action validation, the SB3 Monitor boundary, attempt exclusion/restarts and frozen-estimator mutations. They no longer use unconditional assertions.

Notebook executions are recorded separately in `notebook_execution.json`. Saved outputs show actual results and distinguish historical review from fresh execution. Hosted CI is not claimed to have run locally. The scientific conclusions remain limited by [known limitations](known_limitations.md); this repair does not newly train the full baselines or complete target-conditioned experiments.
