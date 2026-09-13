# Reward Definitions

## TASK Baseline
The TASK objective uses a **score high-water event reward**. The agent receives a reward impulse only when its current score exceeds the highest score seen so far in the current episode.

## MAX Support Baseline
The MAX objective uses a **once-per-fresh-pair q reward**. The agent receives the q-score (increasing-transition support) from the preference model. To prevent farming static states, this reward is delivered exactly once per fresh observation pair, explicitly enforcing stale-output and warm-up behavior constraints.
