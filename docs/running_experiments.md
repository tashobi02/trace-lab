# Running experiments

Complete [setup](setup.md), restore and verify assets, and run offline tests before launching Unity. Use the notebook's declared kernel.

Open the desired notebook under `notebooks/experiments/`. Inspect its resolved settings, set `EXECUTE_NEW_RUN=True`, choose a new permitted attempt, and run the execution cell. TASK/MAX use 51,200 decisions, checkpoints every 10,240 decisions and ten deterministic fresh-process evaluations. The checkpoint smoke uses 4,096 decisions, checkpoints every 2,048 and two evaluations. RANDOM performs ten 600-decision evaluations with PCG64 action seeds 4001–4010 and requested Unity seeds 3001–3010. Active configuration identities are descriptive; archived source IDs remain unchanged for provenance.

A run ID is exclusively reserved beneath `outputs/runs/`. Completed runs, existing attempts and implicit retries are rejected. At most one explicit fresh restart of a recorded failed first attempt is accepted using `RESTART_OF`. Incomplete attempts require diagnosis; they are not silently relabelled failures or resumed. Existing successful smoke validation is retained, so launching the same smoke ID again is intentionally rejected.

The supervisor owns each worker process group, applies configured timeouts, records OS exit status, checks the worker's result and verifies that Unity exited and its port is reusable. Training saves checkpoints after optimization, records parameter changes and fingerprints, and verifies exact decision/rollout counts. Fresh evaluation reloads policy and optimizer states, replays saved-observation actions and confirms no learning occurred.

The telemetry recorder moves the adapter's integer episode ID to `episode_id` before returning info to SB3; raw event files retain the integer. This allows Monitor to own `info['episode']` without collision.

Normal completion, handled interrupts and timeouts have explicit cleanup checks. Browser closure, machine termination or a killed supervisor cannot guarantee cleanup or a recorded exit status. Inspect recorded process ownership and results before recovery. No unrelated process or port is cleared automatically.

Full baseline training is explicit. Merely running a review notebook recalculates or inspects historical evidence and does not train a new policy. Use `outputs/runs/` results to distinguish new measurements from `outputs/reference/` historical measurements.
