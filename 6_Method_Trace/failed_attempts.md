# Failed Attempts

The main difficulty in this project was not getting a result at all, but getting a result that was stable, interpretable, and repeatable across parameter sweeps. A few approaches were tried implicitly during the development process and were not kept in the final version.

## Exact sparse formulation with $L_0$

The ideal sparse formulation would have enforced exact sensor sparsity using an $L_0$ constraint. That was not practical because it would require searching over sensor subsets, which becomes combinatorial very quickly. Even for moderate measurement dimensions, that approach is too expensive for repeated runs and parameter sweeps, so it was replaced by the convex $L_1$ relaxation. This was the first major modeling choice that was ruled out. 

## Fixing one regularization value for all cases

Using one fixed $\lambda$ for all experiments was not a good idea. The plots show that the optimal value depends on the noise level and on whether the system is linear or nonlinear. Small $\lambda$ values leave the corruption insufficiently separated from noise, while large $\lambda$ values over-suppress the corruption term. Because of that, parameter sweeps were necessary instead of a single globally chosen setting. 

## Single-pass nonlinear solving

In the nonlinear case, a direct one-shot solve was not reliable enough because the problem is nonconvex. The pendulum benchmark needed iterative handling through sequential convex programming or a nonlinear solver. Without iteration, the estimates were too sensitive to initialization and local model mismatch. This is why the nonlinear part was split into an OSQP-based iterative method and an IPOPT-based direct method. 

## Overly aggressive regularization in the nonlinear case

For small values of $\lambda$, the nonlinear recovery curves showed more fluctuation across iterations. That behavior suggested that the estimator was not yet separating sparse bias from model mismatch cleanly. Increasing $\lambda$ improved stability, but too much regularization again harmed recovery. So the final version kept the sweep and reported the intermediate region as the useful operating range instead of forcing a single aggressive setting. 

## Expecting OSQP and IPOPT to behave identically

At first, it would be easy to assume that OSQP and IPOPT should give the same convergence behavior. They do not. OSQP is faster per iteration but introduces approximation error through repeated linearization, so the curves can show more oscillation. IPOPT is smoother near the optimum, but it takes longer to run because it solves the full nonlinear constrained problem directly. That runtime cost became noticeable during repeated sweeps. The two solvers agree on the final trend, but not on the speed or path taken to get there. 

## Ignoring the effect of partial observability

Another thing that did not work conceptually was treating the estimation problem as if all states were measured. In the linear case, only half the state is observed directly, so the reconstruction depends strongly on the dynamics and the coupling structure. Ignoring that made the problem look artificially easy. The final setup kept the partial observation structure because it is what makes the sparse recovery problem meaningful in the first place.
