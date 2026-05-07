# LLM Usage Log

## Project / Conversation Scope
This log summarizes how LLM assistance was used for the discussion on sparse bias recovery, OSQP-based SCP optimization, nonlinear pendulum dynamics, Laplacian coupling, and interpretation of parameter-sweep plots.

## External Tools Used

### 1. OpenAI ChatGPT
Used for:
- Reviewing Python code for the λ-sweep plot
- Interpreting the resulting plots and explaining the observed error trends
- Explaining the role of the trust weight in SCP
- Describing the nonlinear dynamics and Laplacian coupling in the model
- Drafting and refining wording for the report-style explanations

## How the Results Were Verified

### Code-level verification
- The plotting function was checked against the surrounding code structure and the expected use of `run_comparison(...)` and `relative_error(...)`.
- The λ sweep logic was reviewed for consistency with the optimization objective and the OSQP workflow.
- The expected effect of the regularization parameter λ was matched against standard L1-sparsity behavior.

### Plot-level verification
- The user-provided plots were inspected qualitatively.
- The observed U-shaped error curve was compared with the expected bias-variance tradeoff for L1 regularization.
- The region where the error saturates near 1 was interpreted as the estimator shrinking the bias vector toward zero, which is consistent with the relative error definition.

### Model / theory consistency check
- The nonlinear dynamics explanation was verified against the stated model form:
  - damped pendulum term with `sin(θ)`
  - Laplacian coupling through neighbor differences
- The trust weight interpretation was checked against its role as a stabilization term for SCP, rather than a sparsity control term.

## Summary
LLM assistance was used as a review and explanation layer rather than as an autonomous source of truth. Final conclusions were validated by checking code logic, matching expected optimization behavior, and comparing the explanations to the user’s observed outputs.