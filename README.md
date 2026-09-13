# Trace Lab

Notebook-based Solid Rally experiments and preparation for trace conditioning. This is a development research repository, not the final thesis repository.

The implemented pipeline verifies frozen native source, player, model and data identities; constructs a matched Unity interface; records decision telemetry; trains supervised PPO TASK/MAX baselines; evaluates saved checkpoints and uniform random actions in fresh processes; reconstructs results; and exports valid window traces.

All maintained Python implementation lives in `.ipynb` files. Code cells retain genuine visible outputs. Imported notebook modules execute only cells tagged `module`; importing them never launches an experiment. The native third-party source is preserved separately as a hashed archive.

Historical development results: TASK and MAX each trained for 51,200 decisions and were evaluated for ten 600-decision episodes; RANDOM has ten episodes. Mean raw scores are 0.0, 0.0 and 0.2; mean valid-pair preference support is 0.277121038, 0.580440079 and 0.412617442, respectively. The analysis reconstructs 7,824 valid comparisons across 202 traces from 32 source event files. See [findings](docs/baseline_findings.md) and [limits](docs/known_limitations.md).

The repaired scorer matches every historical comparison within the original tolerance. A new 4,096-decision notebook-runtime smoke run and two fresh evaluations passed; final policy state, optimizer state and saved-observation actions match the original smoke exactly. This does not claim newly repeated full baseline training. See [verification](docs/verification_report.md).

Start with [setup](docs/setup.md), then [notebook architecture](docs/notebook_architecture.md) and [running experiments](docs/running_experiments.md). Controller notebooks use `trace-lab-controller`; scientific notebooks declare `trace-lab-scientific`. Bulk licensed assets and historical run archives must be supplied locally according to their manifests; they are excluded from Git. Missing assets are a blocking error for dependent checks.
