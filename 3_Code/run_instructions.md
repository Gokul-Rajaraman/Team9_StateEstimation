# Run Instructions

## 1. Create Virtual Environment (Optional)

Using venv:

```bash
python -m venv venv
````

Activate environment:

### Windows

```bash
venv\\Scripts\\activate
```

### Linux / macOS

```bash
source venv/bin/activate
```

---

## 2. Install Dependencies

Install all required libraries using:

```bash
pip install -r requirements.txt
```

---

## 3. Launch Jupyter Notebook

Run:

```bash
jupyter notebook
```

or

```bash
jupyter lab
```

---

## 4. Execute Linear Experiments

Open:

```text
Linear System experiments 2.ipynb
```

Run all cells sequentially.

This notebook:

* Simulates the linear dynamical system
* Injects sparse sensor corruption
* Solves the L1-regularized recovery problem
* Generates recovery plots for:

  * regularization sweep
  * process noise sweep
  * measurement noise sweep

Expected outputs:

* `recovery_error_vs_regularization.png`
* `process_noise_vs_recovery_error (LTI).png`
* `measurement_noise_vs_recovery_error (LTI).png`

---

## 5. Execute Nonlinear Experiments

Open:

```text
nonlinear experiments 1.ipynb
```

Run all cells sequentially.

This notebook:

* Simulates the coupled nonlinear pendulum system
* Injects sparse sensor corruption
* Solves the nonlinear sparse recovery problem using:

  * OSQP
  * IPOPT
* Generates nonlinear recovery plots

Expected outputs:

* `OSQP_recovery_error_vs_regularization (NL).png`
* `IPOPT_recovery_error_vs_regularization (NL).png`
* `OSQP_process_noise_vs_recovery_error (NL).png`
* `OSQP_measurement_noise_vs_recovery_error (NL).png`

---

## 6. Output Storage

Generated plots should be stored in:

```text
4_Data_Results/figures/
```

Numerical outputs may be stored in:

```text
4_Data_Results/outputs/
```

---

## 7. Notes

* Linear experiments execute relatively quickly.
* IPOPT-based nonlinear runs may take significantly longer because the nonlinear constrained optimization problem is solved directly.
* OSQP iterations are faster but may show oscillatory behavior because of repeated local linearization.
* Minor numerical differences between runs are expected because of stochastic noise generation.

```
```
