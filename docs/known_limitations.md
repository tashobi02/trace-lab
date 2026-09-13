# Known limitations

- There is one trained policy per TASK/MAX condition. Ten evaluation episodes are not ten independent training replicates.
- Unity startup seeds reach `UnityRandom.InitState`, but different requested seeds produced identical tested TASK/MAX trajectories. Reset does not reseed Unity. RANDOM has ten distinct recorded trajectories while also changing action RNG seeds; independent simulator diversity remains unproven.
- All 30 development evaluations end at the 600-decision wrapper timeout. Success/completion labels are unavailable and remain NA. A score increase is task progress, not proven task completion.
- q is uncalibrated mean LogisticRegression class-0 increasing-preference support, with per-member MinMax scaling and clipping. It is not measured human affect. Out-of-support clipping is reported.
- Once-per-fresh-pair delivery prevents duplicate reward delivery for the same pair. Newly completed pairs containing repeated or static behavior can still receive q. The evidence includes high-q segments with zero task progress; it does not establish a behavioral cause or a human outcome.
- The historical TASK outer supervisor was interrupted while its worker continued. Training artifacts and all 51,200 decisions were verified, but the original training OS exit status is unavailable. The accounting record preserves this limitation.
- The pinned player was built with Unity 2022.3.62f3. Unity Editor 6000.6.0f1 availability does not establish a compatible rebuild; this repository uses the hashed existing player.
- Full target-conditioned training, calibration bounds, A/B/CONST controls and the final evaluation protocol remain future work. The current 39 valid pairs are odd: 38 pairs imply 117 seconds, while 40 imply 123 seconds beyond the current 120-second horizon. No target/horizon choice is made here.
- The new runtime validation repeats the 4,096-decision smoke and checkpoint evaluations. Full 51,200-decision TASK/MAX results shown here are reconstructed historical evidence, not newly retrained baselines.
