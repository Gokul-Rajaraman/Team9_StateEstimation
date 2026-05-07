# Design Decisions

This project was built around a sparse corruption recovery setting, where the main goal was to estimate the hidden state of a dynamical system while also identifying a small number of corrupted sensors. The core modeling choice was to treat corruption as a sparse additive term in the measurement equation rather than as generic noise. That decision was important because the experimental plots show that the estimator behaves differently when corruption is sparse and persistent compared to when the disturbance is only random measurement noise. 

## Linear model choices

For the linear experiments, the system was kept deliberately structured. The dynamics matrix was chosen to be stable and tridiagonal so that the open-loop trajectory stayed bounded and the state coupling remained interpretable. Only half of the states were measured directly, using a partial observation matrix of the form \([I\ 0]\). This made the reconstruction problem nontrivial but still manageable, because the unmeasured states had to be inferred through the system dynamics. The input was included in simulation, while the estimation stage focused on recovering the state and corruption from measurements. :contentReference[oaicite:1]{index=1}

The corruption model was fixed over a small number of sensors, rather than changing randomly at every time step. This made the corruption behave more like a persistent sensor bias, which is closer to a faulty channel than a one-off spike. That choice also matches the recovery plots, where the estimator is able to isolate the biased sensors only when the regularization is neither too weak nor too strong. 

The linear recovery problem was formulated in batch form with an \(L_1\) penalty on the corruption term. An exact \(L_0\) formulation was not used because it would require combinatorial search over sensor subsets and would not scale well. The \(L_1\) relaxation gave a convex problem that could be solved reliably with standard optimization tools. This was the right tradeoff for the project because the objective was not only accuracy, but also having a method that could be run repeatedly during parameter sweeps.

## Why the regularization sweep was central

The regularization parameter \(\lambda\) was treated as the main tuning knob because it directly controls the balance between sparsity and data fit. The plots show a clear U-shaped trend: very small \(\lambda\) under-regularizes and allows corruption to leak into the state estimate, while very large \(\lambda\) over-penalizes the bias term and suppresses valid corruption. The intermediate region gives the best recovery, so the sweep was necessary to identify a sensible operating point instead of fixing \(\lambda\) arbitrarily. 

## Nonlinear model choices

The nonlinear benchmark was chosen to make the problem more realistic without losing structure. A coupled damped pendulum chain was used because it has nonlinear restoring torque, local neighbor coupling, and partial observability, all of which make sparse recovery harder in a meaningful way. The state was split into angles and angular velocities, and coupling was introduced through a Laplacian matrix. This gave a benchmark where local disturbances can spread across the network, so corruption in one sensor can affect the reconstructed trajectory more broadly.

The same sparse measurement model was retained in the nonlinear case so that the comparison with the linear system stayed clean. The main difference was that the dynamics were now nonconvex, so the estimator had to be handled iteratively rather than in a single convex solve. That is why the nonlinear part was solved using both sequential convex programming with OSQP and direct nonlinear optimization with IPOPT. 

## Why OSQP and IPOPT were both used

OSQP was used because it fits the sequential convex programming approach well. The nonlinear dynamics can be linearized around the current iterate, giving a sequence of quadratic subproblems that are computationally efficient to solve. This made OSQP the faster option for repeated sweeps. IPOPT was included as a direct nonlinear benchmark, so the same objective could be tested without relying on repeated linearization. That comparison was useful because it showed that the sparse recovery trend was not solver-specific. Both solvers still produced the same broad U-shaped dependence on \(\lambda\). 

## Why the final plots look the way they do

The shapes of the curves were not accidental. In the linear case, the recovery error decreases to a minimum at moderate regularization and then rises again, which is the expected sparse-penalty tradeoff. The process-noise and measurement-noise curves both rise with noise level because the estimator has a harder time separating structured corruption from random disturbance. In the nonlinear case, the same trends appear, but the curves are less clean because the dynamics are more sensitive and the optimization is nonconvex. The OSQP curves show more oscillation during the iterative updates, while IPOPT is smoother but slower to run. 