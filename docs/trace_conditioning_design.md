# Trace Conditioning Design (Future Extension)

This outlines the intended design for trace-conditioning workflows.

### Planned Notebooks
- **Library**: `target_schedules.ipynb`, `trace_similarity_reward.ipynb`
- **Calibration**: `define_calibration_data.ipynb`, `select_target_support.ipynb`, `validate_target_timing.ipynb`
- **Experiments**: `run_trace_forward.ipynb`, `run_trace_reverse.ipynb`, `run_trace_constant.ipynb`
- **Analysis/Verification**: `compare_trace_tracking.ipynb`, `verify_target_schedules.ipynb`, `verify_trace_rewards.ipynb`

### Unresolved Decisions
- Target calibration bounds.
- Even-pair horizon decisions for comparison counts (current 39 valid pairs is odd).
