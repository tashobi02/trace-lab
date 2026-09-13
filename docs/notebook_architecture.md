# Notebook Architecture

Trace-lab uses a notebook-first architecture. Notebooks act as the entry points and reusable implementation units.
There are four primary notebook types:
1. **Library**: Define reusable functions and classes (e.g., `preference_scoring.ipynb`).
2. **Experiment**: Configure, validate and supervise a complete experiment (e.g., `run_task_baseline.ipynb`).
3. **Worker**: Execute one training job or evaluation episode in a fresh kernel (e.g., `train_policy.ipynb`).
4. **Analysis or Verification**: Read saved evidence, calculate results, and check correctness (e.g., `verify_rewards.ipynb`).
