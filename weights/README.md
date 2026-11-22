# Initial network weights

These arrays describe the networks immediately before the first gradient update in the experiments of Section V. They use binary64 precision. Each JSON object maps a tensor name to a nested numeric array, with no framework-specific serialization.

## Choosing the files

Use `actor_common.json` for all runs. For each of the ten paired learning-efficiency runs, use the matching `critic_seed_01.json` through `critic_seed_10.json`. Residual-based RL and fixed-reward RL started with identical actor and critic arrays within each pair.

Use `critic_seed_17.json` with the same actor for the separate tracking and disturbance-rejection example. This is the update-0 initialization for the policies evaluated after 1,886 updates. The supervised-only controller used the same initial actor. Its actor update used the supervised term alone.

## Array contents

| File | Key | Shape | Meaning |
|---|---|---|---|
| Actor | `coefficients` | 2 × 11 | Trainable coefficients of the two-output mechanical-basis actor |
| Actor | `coefficient_scales` | 2 × 11 | Fixed scale factors for the two coefficient rows |
| Actor | `whitener` | 2 × 11 × 11 | Prepared, fixed basis transformation for each row |
| Actor | `output_map` | 2 × 2 | Fixed output transformation |
| Critic | `net.0.weight`, `net.0.bias` | 32 × 18, 32 | First hidden layer |
| Critic | `net.2.weight`, `net.2.bias` | 32 × 32, 32 | Second hidden layer |
| Critic | `net.4.weight`, `net.4.bias` | 1 × 32, 1 | Scalar output layer |
| Critic | `features.scale`, `u_scale` | 4, 2 | Fixed physical-state and action normalization scales |

The critic has tanh hidden activations. Its 18 inputs comprise the scaled plant state, scaled reference state, eight reference-context components and two scaled actions. Weight matrices are indexed by output unit first and input unit second.

## Provenance and checks

For paired run seed s from 1 to 10, the critic initialization seed was s and the CUDA training-sample generator seed was 20,260 + s. The separate run used critic seed 17 and restored its own prepared CUDA sampling state at update 0 (generator seed 185,901 and offset 768).

All arrays were extracted from archived update-0 network states. Each array was parsed from the exported JSON as binary64 and checked byte-for-byte against its source tensor. The paired initializations were also matched against an independent experiment archive. For the separate run, its archived RL, supervised and fixed-reward initial network states were compared directly.
