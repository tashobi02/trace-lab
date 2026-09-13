# Development baseline findings

| Condition | Training decisions | Evaluations | Mean raw score | Mean q | Zero-progress episodes |
|---|---:|---:|---:|---:|---:|
| TASK | 51,200 | 10 | 0.0 | 0.277121038 | 10 |
| MAX | 51,200 | 10 | 0.0 | 0.580440079 | 10 |
| RANDOM | 0 | 10 | 0.2 | 0.412617442 | 8 |

Both trained conditions used 25 PPO rollouts of 2,048 decisions. TASK training records five task-progress events; MAX records twelve. Their 86 recorded training episodes each include 85 full episodes and a final 200-decision collection fragment. Training returns and evaluation results are separate quantities.

All evaluations have 600 decisions and 39 valid pairs, with 100% eligible-pair coverage. All end by wrapper timeout; completion labels are NA. TASK and MAX each repeat one recorded evaluation trajectory despite differing requested Unity seeds. RANDOM scores one on requested seeds 3004 and 3006 and zero on the others.

The six inspected segments include a MAX high-q, zero-progress segment at decisions 226–285 for requested seed 3001. This shows separation between preference support and task progress, not a demonstrated explanation for the behavior.

`compare_baselines.ipynb` reconstructs all 18,000 evaluation decisions and 1,170 evaluation pairs from raw events. The complete export adds 6,654 training pairs, giving 7,824 pairs across 202 traces. Tables and four PNG/PDF figure families are saved under `evidence/baselines/solid_rally_development/`; generated recalculations live in `outputs/analysis/`.
