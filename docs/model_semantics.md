# Model Semantics

The preference scoring model relies on five `LogisticRegression` members trained to detect increasing-transition support (class 0).
Scaling and clipping are handled by frozen `StandardScaler` artifacts for reproducibility.
