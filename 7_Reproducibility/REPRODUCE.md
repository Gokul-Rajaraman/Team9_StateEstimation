# Repository / Archive Link

GitHub Repository:
https://github.com/Gokul-Rajaraman/Team9_StateEstimation

# Reproducing the Results

This document describes the steps required to reproduce the main results for the project:
**Sparse State Estimation Under Sensor Corruption**

The project contains two sets of experiments:
1. Linear sparse state estimation
2. Nonlinear sparse estimation using a coupled pendulum network

---

# 1. Project Structure

```text
3_Code/
├── src/
├── notebooks/
├── requirements.txt
└── run_instructions.md
````

Main notebooks used:

```text
Linear System experiments 2.ipynb
nonlinear experiments 1.ipynb
```

---

# 2. Running Linear Experiments

Open and execute:

```text
Linear System experiments 2.ipynb
```

The notebook performs the following steps:

1. Generates a stable partially observed linear dynamical system
2. Simulates the state trajectory over the chosen horizon
3. Injects sparse sensor corruption
4. Adds Gaussian process and measurement noise
5. Solves the sparse recovery problem using L1-regularized optimization
6. Sweeps the regularization parameter λ
7. Sweeps process noise σw
8. Sweeps measurement noise σv
9. Generates plots used in the report

---

## Expected Outputs

### Regularization Sweep

Generated figure:

```text
recovery_error_vs_regularization.png
```

Expected trend:

* U-shaped recovery curve
* Best recovery at intermediate λ
* Small λ under-regularizes corruption
* Large λ suppresses sparse bias excessively

### Process Noise Sweep

Generated figure:

```text
process_noise_vs_recovery_error (LTI).png
```

Expected trend:

* Recovery error increases gradually with process noise

### Measurement Noise Sweep

Generated figure:

```text
measurement_noise_vs_recovery_error (LTI).png
```

Expected trend:

* Recovery error increases with measurement noise
* Small fluctuations may appear because of random trials

---

# 3. Running Nonlinear Experiments

Open and execute:

```text
nonlinear experiments 1.ipynb
```

The notebook performs the following steps:

1. Simulates the coupled damped pendulum network
2. Generates nonlinear trajectories
3. Injects sparse sensor corruption
4. Adds process and measurement noise
5. Solves the nonlinear sparse recovery problem using:

   * Sequential convex programming with OSQP
   * Direct nonlinear optimization with IPOPT
6. Sweeps λ, σw, and σv
7. Generates recovery plots

---

## Expected Outputs

### OSQP Regularization Sweep

Generated figure:

```text
OSQP_recovery_error_vs_regularization (NL).png
```

Expected trend:

* U-shaped recovery curve
* Oscillatory behavior for smaller λ
* Best recovery at moderate λ

### IPOPT Regularization Sweep

Generated figure:

```text
IPOPT_recovery_error_vs_regularization (NL).png
```

Expected trend:

* Similar U-shaped trend
* Smoother convergence behavior
* Longer runtime compared to OSQP

### Process Noise Sweep

Generated figure:

```text
OSQP_process_noise_vs_recovery_error (NL).png
```

Expected trend:

* Recovery error increases gradually with σw

### Measurement Noise Sweep

Generated figure:

```text
OSQP_measurement_noise_vs_recovery_error (NL).png
```

Expected trend:

* Recovery error increases with σv
* Curves remain relatively smooth

---

# 4. Output Storage

Generated plots should be stored in:

```text
4_Data_Results/figures/
```

Important numerical outputs may be stored in:

```text
4_Data_Results/outputs/
```

---

# 5. Notes

* Linear experiments execute comparatively faster.
* IPOPT-based nonlinear runs may require significantly longer runtime because the full nonlinear constrained optimization problem is solved directly.
* OSQP iterations are faster but may show oscillatory behavior due to repeated local linearization.
* Minor numerical differences between runs are expected because of random initialization and stochastic noise generation.

---

# 6. Verification

The generated plots should qualitatively match the figures included in:

```text
1_Report/
```

Key trends that should appear:

* U-shaped regularization curves
* Increasing recovery error with larger process noise
* Increasing recovery error with larger measurement noise
* Similar sparsity behavior across OSQP and IPOPT

```
```
