# Running Experiments

## Execution Flow
1. **Experiment Notebook**: The user opens and executes an experiment notebook (e.g. `run_task_baseline.ipynb`).
2. **Supervisor**: The notebook validates inputs, resolves configurations, and safely registers a new attempt.
3. **Workers**: The supervisor executes worker notebooks (`train_policy.ipynb`, `evaluate_policy_episode.ipynb`) via fresh isolated kernels.
4. **Cleanup & Results**: The workers save checkpoints, telemetry, and execution statuses. Once complete, the experiment notebook renders the results.

This structure guarantees that closing a browser tab does not corrupt the run. Failures and interrupts strictly leave accurate diagnostic records and enforce Unity cleanup.
