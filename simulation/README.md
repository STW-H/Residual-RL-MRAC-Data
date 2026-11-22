# Manipulator simulation results

These files contain the trajectories and tracking-error statistics for Figures 3 and 4 and Tables II and III. They use the separate run with critic initialization seed 17. Each controller was frozen after 1886 learning updates. The sampling interval is 0.02 s. Joint angles are measured in radians and angular velocities in radians per second. Both joints start at rest, with initial angles of 0.05 and -0.05 rad.

| File | Contents |
|---|---|
| [tracking.csv](tracking.csv) | Figure 3. One row for each of the 1001 timestamps from 0 to 20 s. The columns give the reference and the simulated trajectories for residual-based RL, supervised learning (SL) and fixed-reward RL with threshold 0.02. Each set of four columns gives joint angles 1 and 2 followed by angular velocities 1 and 2. |
| [table_ii.csv](table_ii.csv) | Table II. Per-state RMSE for the three methods. The unit column gives mrad for angles and mrad/s for velocities. |
| [compensation.csv](compensation.csv) | Figure 4 and Table III. Each row gives four signed errors (simulated state minus reference) for one torque condition, controller and timestamp. The joint-angle error norm in mrad is 1000 times the Euclidean norm of the two angle-error columns. |
| [table_iii.csv](table_iii.csv) | Table III. For each torque condition, the first three RMSE columns report joint angles (mrad) and the last three report angular velocities (mrad/s). Controllers within each group appear in the order RL only, RL with SMC and RL with EID. |

All compensation comparisons use the same frozen residual-based RL actor. Both compensators operate from startup. The four torque conditions are no external torque (residual only), a slow sinusoid, a step at 10 s and a fast sinusoid. The file labels them `residual_only`, `slow_sine`, `torque_step` and `fast_sine`. The three controller labels are `rl_only`, `rl_smc` and `rl_eid`.

For Table II, subtract the reference column from each corresponding state column and compute the square root of the mean squared error over time. For Table III, average the squared errors over both joints and all timestamps in the window, separately for angles and velocities, then take the square root. Multiply by 1000 to express the results in mrad or mrad/s.

The 1–20 s interval contains 951 samples. For the step condition in Table III, the 11–20 s interval contains 451 samples. Both endpoints are included. The summary CSVs report additional digits. All 36 table entries were recomputed from the released trajectory CSVs and agree with the manuscript at five decimal places.
