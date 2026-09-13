# Environment Contract

Defines the common observation/action interface for the Solid Rally Unity environment.
Includes 81 native fields + normalized time, q, valid, fresh, and normalized age.
Action space uses `MultiDiscrete([3,3])` which is mapped to native `[steering, pedal, 0]`.
Reset behavior and explicit valid/fresh information are strictly defined to guarantee isolation.
