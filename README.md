# Sparse State Estimation Under Sensor Corruption

## Project Overview
This project studies robust state estimation in the presence of sparse sensor corruption for both linear and nonlinear dynamical systems. The linear benchmark uses a partially observed discrete-time state-space model with process noise, measurement noise, and sparse persistent sensor bias. The nonlinear benchmark extends the same idea to a coupled damped pendulum network and compares sequential convex programming (OSQP) with direct nonlinear optimization (IPOPT).

The main deliverables include the IEEE-format final report, presentation slides, source code, plotted results, literature references, method trace notes, and reproducibility instructions.

## Folder Structure
```text
TeamName_ProjectTitle/
├── 1_Report/
├── 2_Presentation/
├── 3_Code/
├── 4_Data_Results/
├── 5_Literature/
├── 6_Method_Trace/
├── 7_Reproducibility/
└── README.md
```

### 1_Report/
Contains the final IEEE double-column report in PDF format along with the source file used to generate it, either LaTeX or Word.

### 2_Presentation/
Contains the final presentation slides in PDF or PPT format. A short demo video may also be included if available.

### 3_Code/
Contains the implementation used for the experiments.
Recommended structure:
```text
Code/
├── src/
├── notebooks/
├── requirements.txt / environment.yml
└── run_instructions.md
```

### 4_Data_Results/
Contains the data and outputs used in the project.
Recommended structure:
```text
Data_Results/
├── input_data/
├── processed_data/
├── outputs/
└── figures/
```
The final plots used in the report should be placed in `figures/`, and important numeric outputs should be placed in `outputs/`.

### 5_Literature/
Contains 5 to 10 relevant papers used for background study, along with short summaries of each paper.

### 6_Method_Trace/
Contains the design decisions, failed attempts, and tool usage notes that describe how the project evolved.
Recommended files:
```text
Method_Trace/
├── design_decisions.md
├── failed_attempts.md
└── llm_usage_log.md
```

### 7_Reproducibility/
Contains instructions for reproducing the results, along with a GitHub or Zenodo link if provided.
Recommended file:
```text
REPRODUCE.md
```

## How to Run the Code
1. Install the required dependencies using `requirements.txt` or `environment.yml`.
2. Open the notebooks in `3_Code/notebooks/` or run the main script from `3_Code/src/`.
3. Generate the linear and nonlinear experiment outputs.
4. Saved figures should appear in `4_Data_Results/figures/`.

Example commands:
```bash
pip install -r requirements.txt
python src/main.py
```

If an environment file is used:
```bash
conda env create -f environment.yml
conda activate <env_name>
python src/main.py
```

## Main Results
The main results are stored in `4_Data_Results/figures/` and correspond to:
- Linear recovery error versus regularization
- Linear recovery error versus process noise
- Linear recovery error versus measurement noise
- Nonlinear OSQP recovery error versus regularization
- Nonlinear IPOPT recovery error versus regularization
- Nonlinear recovery error versus process noise
- Nonlinear recovery error versus measurement noise

The final report in `1_Report/` explains these results in detail.

## Notes
- The project focuses on sparse corruption recovery using L1-regularized estimation.
- The linear case provides the baseline convex formulation.
- The nonlinear case studies a more realistic coupled pendulum system and compares OSQP and IPOPT.

