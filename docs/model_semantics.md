# Frozen preference model

The actual five fitted members are `sklearn.linear_model.LogisticRegression`; their five fitted scalers are `sklearn.preprocessing.MinMaxScaler`. `configs/preference_model.yaml` records these names, target class 0 and all 54 ordered features: 27 L-window means followed by 27 R-window means.

For each member, apply its stored scaler, clip the scaled input to [0,1], and take class-0 support. q is the mean across five members. Class order must be [0,1]; class 0 denotes increasing preference in this archived dataset contract. This is uncalibrated model support, not a human affect measurement.

The scorer rejects incomplete ensembles, wrong feature dimensions, nonfinite inputs and mutated fitted state. Its numerical output is checked against all 7,824 original valid pairs and an independent affine/logit calculation. Omitting clipping formerly caused 331 mismatches; repaired scoring has zero mismatches at atol=1e-6, rtol=1e-5, maximum residual 3.33e-16.
