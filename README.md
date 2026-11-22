# Residual-RL-MRAC-Data

This repository contains the initial neural network weights and simulation data for the algorithm comparisons in Section V of *Residual-Based Reinforcement Learning for Model Reference Adaptive Control of Nonlinear Cyber-Physical Systems*.

The learning experiments compare residual-based reinforcement learning (RL) with fixed-threshold RL across ten paired runs. A separate tracking experiment compares both RL methods with supervised learning. The disturbance-rejection experiment uses the same frozen residual-based controller to compare equivalent-input-disturbance (EID) compensation, sliding-mode control (SMC), and operation without compensation.

**Source code coming soon.**

| Paper result | Data |
|---|---|
| Learning efficiency for seeds 1–10 | [First update satisfying the residual bound](learning/first_residual_bound.csv) |
| Actor and critic initialization | [Weight arrays, tensor shapes and seed mapping](weights/README.md) |
| Tracking and disturbance rejection for seed 17, Figures 3–4 and Tables II–III | [Time histories, RMSE tables, units and evaluation windows](simulation/README.md) |
| Seed 17 certification, EID activation and parameter sensitivity | [Supplementary results](supplementary/README.md) |

## Reading the learning results

Each row in the learning CSV identifies a seed and a reward design. Within a pair, residual-based RL and fixed-reward RL (threshold 0.02) shared the same initial weights and training samples. Each update used 512 state–reference pairs. Both RL methods used an actor weight of η = 0.0003 for the RL term and a discount factor of 0.97.

`first_pass_update` counts updates through the first verified satisfaction of the residual bound over the full operating region. For a passing run, `last_observed_update` gives the first pass because observation for this comparison stops there. An empty first-pass field and `right_censored` indicate that the bound had yet to be met at the reported observation horizon.

Residual-based RL first passed after 1,663–2,055 updates (mean 1,886.7). Fixed-reward RL first passed at 2,520 and 2,602 updates for seeds 2 and 3, respectively. For the other eight seeds the residual check had yet to pass at update 26,600.

## Checking the tracking results

The tracking and disturbance-rejection figures use an independent run with critic initialization seed 17. All three actors were frozen at update 1,886 for this comparison. The simulation files give the reference trajectory, state trajectories and compensation errors at 0.02 s intervals. The [simulation notes](simulation/README.md) specify the averaging windows and equations for recomputing all 36 RMSE values in Tables II and III.

The [SHA-256 manifest](SHA256SUMS.txt) lists the digest of each data and documentation file. This release carries no separate reuse license.
