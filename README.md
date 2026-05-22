# **`README.md`**

# Optimal Investment and Pension Policy in PAYG Systems: An Empirical Replication Pipeline

<!-- PROJECT SHIELDS -->
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/python-3.10%2B-blue.svg)](https://www.python.org/)
[![arXiv](https://img.shields.io/badge/arXiv-2605.12698-b31b1b.svg)](https://arxiv.org/abs/2605.12698)
[![Journal](https://img.shields.io/badge/Journal-ArXiv%20Preprint-003366)](https://arxiv.org/abs/2605.12698)
[![Year](https://img.shields.io/badge/Year-2026-purple)](https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems)
[![Discipline: Math Finance](https://img.shields.io/badge/Discipline-Mathematical%20Finance-00529B)](https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems)
[![Discipline: Actuarial](https://img.shields.io/badge/Discipline-Actuarial%20Science-00529B)](https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems)
[![Discipline: Control](https://img.shields.io/badge/Discipline-Stochastic%20Control-00529B)](https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems)
[![Data: Eurostat](https://img.shields.io/badge/Data-Eurostat%20Earnings-lightgrey)](https://ec.europa.eu/eurostat)
[![Data: OECD](https://img.shields.io/badge/Data-OECD%20Pensions-lightgrey)](https://www.oecd.org/)
[![Method: Forward Utility](https://img.shields.io/badge/Method-Forward%20Utility-orange)](https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems)
[![Method: Euler-Maruyama](https://img.shields.io/badge/Method-Euler--Maruyama-orange)](https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems)
[![Method: Cholesky](https://img.shields.io/badge/Method-Cholesky%20Decomposition-orange)](https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Type Checking: mypy](https://img.shields.io/badge/type%20checking-mypy-blue)](http://mypy-lang.org/)
[![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=flat&logo=numpy&logoColor=white)](https://numpy.org/)
[![SciPy](https://img.shields.io/badge/SciPy-%230C55A5.svg?style=flat&logo=scipy&logoColor=white)](https://scipy.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-%23F37626.svg?style=flat&logo=Jupyter&logoColor=white)](https://jupyter.org/)
[![YAML](https://img.shields.io/badge/YAML-%23CB171E.svg?style=flat&logo=yaml&logoColor=white)](https://yaml.org/)
[![Open Source](https://img.shields.io/badge/Open%20Source-%E2%9D%A4-brightgreen)](https://github.com/chirindaopensource/framework_for_high_volume_procurement_oversight_and_decision_support)

**Repository:** `https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems`

**Owner:** 2026 Craig Chirinda (Open Source Projects)

## Introduction

This project is an independent, professional-grade implementation of the ideas and mathematical methodologies from the paper titled **"Optimal investment and Pension policy in Pay-As-You-Go systems under forward utility and ageing population"** by the authors:
*   **Jennifer Alonso-Garcia**
*   **Caroline Hillairet**
*   **Sarah Kaakai**
*   **Mohamed Mrad**

This repository provides a complete, end-to-end computational framework for replicating the paper's findings. It delivers a highly optimized, causally consistent pipeline that simulates a hybrid Pay-As-You-Go (PAYG) pension system supplemented by a market-invested buffer fund. By utilizing **forward Constant Relative Risk Aversion (CRRA) utilities**, the codebase establishes a time-consistent optimal control architecture that dynamically balances benefit adequacy for current retirees against the long-term solvency required for future generations, particularly under the stress of systemic demographic ageing (the "Baby Boom" transition).

## Table of Contents

- [Introduction](#introduction)
- [Theoretical Background](#theoretical-background)
- [Features](#features)
- [Methodology Implemented](#methodology-implemented)
- [Core Components (Notebook Structure)](#core-components-notebook-structure)
- [Key Callable: execute_master_orchestrator](#key-callable-execute_master_orchestrator)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Input Data Structure](#input-data-structure)
- [Usage](#usage)
- [Output Structure](#output-structure)
- [Project Structure](#project-structure)
- [Customization](#customization)
- [Contributing](#contributing)
- [Recommended Extensions](#recommended-extensions)
- [License](#license)
- [Citation](#citation)
- [Acknowledgments](#acknowledgments)

## Theoretical Background

The implemented methods bridge continuous-time stochastic optimal control with discrete numerical simulation.

**1. The 4D Stochastic Market Environment:**
The system operates in an incomplete market driven by a 4-dimensional correlated Brownian motion $B = {}^t(B^S, B^\nu, B^r, B^e)$. The risky asset follows a Heston stochastic volatility model, the interest rate follows a Vasicek model, and wages follow a geometric Brownian motion. The correlation structure is defined by $\Gamma = L {}^tL$.

**2. The Hybrid PAYG Framework:**
The buffer fund $F_t$ receives contributions $C_t = \alpha e_t N_t^w$ and pays out pensions $P_t = p_t N_t^r$. The system must satisfy an adequacy constraint (pensions cannot fall below the pure PAYG level $p_t^{min}$) and a sustainability constraint (the fund cannot breach a debt floor $K_t$).

**3. Forward Utility and Time-Consistency:**
To avoid the horizon-dependence of traditional backward Bellman equations, the social planner's preferences are modeled using forward CRRA utilities. The weight assigned to the buffer fund, $Z_t^u$, evolves dynamically according to a non-linear Hamilton-Jacobi-Bellman (HJB) consistency SDE:
$$ dZ_t^u = Z_t^u \left( - \left[ (1-\theta)r_t + \frac{1-\theta}{2\theta} (({}^tL\delta_t)_S + \eta_t)^2 + \theta N_t^r \left( \frac{Z_t \omega_t}{Z_t^u} \right)^{1/\theta} \right] dt + \delta_t \cdot dB_t \right) $$

**4. Optimal Control Laws:**
The pipeline implements the closed-form feedback laws derived in Theorem 3.2. The optimal pension payout $p_t^*$ distributes a surplus proportional to the fund's cushion, scaled by the ratio of current retiree weights to the dynamic buffer weight:
$$ p_t^* = p_t^{min} + (F_t^* - K_t) \left( \frac{Z_t \omega_t}{Z_t^u} \right)^{1/\theta} \mathbf{1}_{\{t < \tau^Z\}} $$

Below is a diagram which summarizes the proposed approach:

<div align="center">
  <img src="https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems/blob/main/optimal_investment_and_pension_policy_in_pay_as_you_go_systems_ipo_main.png" alt="Pension Policy Architecture" width="100%">
</div>

## Features

-   **Causal State-Space Integration:** Resolves the circular dependencies inherent in the optimal control rules by integrating the HJB-consistency SDE, the policy laws, and the buffer fund dynamics in a single, sequential Euler-Maruyama loop.
-   **Strict Memory Management:** Pre-allocates 2D matrices and immediately downsamples high-frequency paths (4,801 state points) to an annual reporting grid during Monte Carlo simulations, preventing Out-Of-Memory (OOM) crashes.
-   **Deterministic Common Random Numbers (CRN):** Utilizes `numpy.random.SeedSequence` to spawn independent entropy streams, guaranteeing that demographic comparisons (Steady State vs. Baby Boom) are evaluated against mathematically identical market shocks.
-   **Robust Root-Finding:** Implements Brent's method with deterministic bracket expansion to solve the Equivalent Annual Indexation Rate (EAIR) polynomial across highly volatile simulated cashflows.
-   **Immutable Data Structures:** Employs frozen `dataclasses` extensively to prevent parameter drift, ensuring perfect auditability and reproducibility across the experimental matrix.

## Methodology Implemented

1.  **Data Ingestion & Validation:** Validates the temporal grid ($T=40, \Delta t=1/120$) and enforces strict demographic identities ($N_t^r = DR_t N_t^w$).
2.  **Stochastic Simulation:** Generates the 4D correlated Brownian increments via Cholesky decomposition and simulates the exogenous market states (Heston, Vasicek, Wages).
3.  **Preference Calibration:** Inverts the optimal pension rule at $t=0$ to calibrate the initial forward utility weight ($Z_0^u$) to a targeted 5% initial generosity surplus.
4.  **Policy Integration:** Executes the fused Euler-Maruyama loop to jointly evolve the planner's preferences and the buffer fund wealth.
5.  **Depletion Detection:** Enforces absorbing boundaries ($F_t \le K_t$ or $Z_t^u \le 0$) and applies strict post-depletion reversion rules ($p_t^* = p_t^{min}$, $\pi_t^* = 0$).
6.  **Evaluation & Diagnostics:** Computes EAIR, Benefit Ratios, and rigorously validates theoretical invariants, such as the independence of the depletion time $\tau$ from the initial fund level $F_0$.

## Core Components (Notebook Structure)

*Note: All 35+ orchestrator callables and their constituent helper functions are contained within a singular, comprehensive Jupyter Notebook.*

The notebook is structured as a logical Directed Acyclic Graph (DAG), moving from raw data ingestion and validation, through stochastic market generation, forward utility calibration, causal policy integration, and final theoretical bounding and evaluation.

## Key Callable: `execute_master_orchestrator`

The project is designed around a single, top-level user-facing interface function:

-   **`execute_master_orchestrator`:** This apex orchestrator function runs the entire automated research pipeline from end-to-end. A single call to this function reproduces the entire computational portion of the project. It manages the freezing of the research environment, executes the pathwise illustrative runs, orchestrates the 10,000-path Monte Carlo simulations with CRN, conducts the $\delta$, $Z_0^u$, and $\theta$ sensitivity analyses, and performs the final Verification and Validation (V&V) checks. It returns a comprehensive dictionary containing all generated artifacts, tables, figures, and certification reports.

## Prerequisites

-   Python 3.10+
-   Core Python dependencies: `numpy`, `pandas`, `scipy`, `matplotlib`, `pyyaml`, `Faker`.

## Installation

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems.git
    cd optimal_investment_and_pension_policy_in_pay_as_you_go_systems
    ```

2.  **Create and activate a virtual environment (recommended):**
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install Python dependencies:**
    ```sh
    pip install numpy pandas scipy matplotlib pyyaml Faker
    ```

## Input Data Structure

The pipeline requires two primary inputs:
1.  **`raw_demographics` (pd.DataFrame)**: Contains the continuous model-time index ($t_n$) and the deterministic exogenous demographic paths ($N_t^w$, $N_t^{r,SS}$, $DR_t^{SS}$, $N_t^{r,BB}$, $DR_t^{BB}$) evaluated exactly on the Euler simulation grid.
2.  **`config.yaml`**: The master configuration file containing all SDE coefficients, forward utility preference parameters, numerical tolerances, and Monte Carlo controls.

## Usage

Here is the granular, step-by-step guide to executing the end-to-end pipeline. This example demonstrates how to synthetically generate the required demographic trajectories on the exact Euler grid, load the study configuration from the YAML file, and execute the full research pipeline using the `execute_master_orchestrator` function.

*Note: As per the architectural constraints of this environment, we assume that all the callables defined previously in this conversation are already loaded into memory within a single Jupyter Notebook. There is no reliance on external `.py` module imports for the pipeline functions. We also assume `config.yaml` is saved in the working directory.*

```python
import pandas as pd
import numpy as np
import yaml
import os
from typing import Dict, Any

# Initialize random seed for any stochastic elements (though demographics are deterministic here)
np.random.seed(42)

def generate_synthetic_demographics_data(
    horizon_years: float = 40.0,
    dt: float = 1.0 / 120.0
) -> pd.DataFrame:
    """
    Generates a synthetic demographic DataFrame on the exact Euler simulation grid.

    Purpose:
        To create a high-fidelity, mathematically plausible dataset that mimics the 
        exogenous demographic shocks required by the study. This provides the 
        Temporal and Demographic Input Architecture for the master orchestrator.

    Inputs:
        horizon_years (float): The total simulation horizon T. Default is 40.0.
        dt (float): The Euler discretization time step \Delta t. Default is 1/120.

    Processes:
        1. Grid Generation: Calculates the number of state points (N_state = T/dt + 1) 
           and generates the continuous time vector t_n.
        2. Worker Population: Fixes N_t^w = 100.0 across all t.
        3. Steady State (SS): Fixes DR_t^{SS} = 0.3 and computes N_t^{r,SS}.
        4. Baby Boom (BB): Generates a linear trend for DR_t^{BB} from 0.3 to 0.5 
           and computes N_t^{r,BB}.
        5. Schema Enforcement: Casts all arrays to float64.

    Outputs:
        pd.DataFrame: A DataFrame containing the exact columns required by the schema.

    Raises:
        ValueError: If horizon_years or dt are zero or negative.
    """
    # Validate input parameters to prevent mathematical domain errors
    if horizon_years <= 0.0 or dt <= 0.0:
        raise ValueError("horizon_years and dt must be strictly positive floats.")

    # 1. Calculate the exact number of state points required for the Euler grid
    n_state_points = int(round(horizon_years / dt)) + 1

    # Generate the continuous model time in years: t_n = n * \Delta t
    t_years = np.linspace(0.0, horizon_years, n_state_points, dtype=np.float64)

    # 2. Generate the constant worker population: N_t^w = 100
    nw_t = np.full(n_state_points, 100.0, dtype=np.float64)

    # 3. Generate the Steady State (SS) trajectories
    dr_t_ss = np.full(n_state_points, 0.3, dtype=np.float64)
    nr_t_ss = np.full(n_state_points, 30.0, dtype=np.float64)

    # 4. Generate the Baby Boom (BB) trajectories
    dr_t_bb = np.linspace(0.3, 0.5, n_state_points, dtype=np.float64)
    # Note: We strictly avoid integer casting here to maintain SDE precision
    nr_t_bb = dr_t_bb * nw_t

    # 5. Construct the DataFrame and enforce the schema
    raw_demographics = pd.DataFrame({
        "t_years": t_years,
        "Nw_t": nw_t,
        "DR_t_SS": dr_t_ss,
        "Nr_t_SS": nr_t_ss,
        "DR_t_BB": dr_t_bb,
        "Nr_t_BB": nr_t_bb
    })

    return raw_demographics

# Generate the synthetic demographic dataset
raw_demographics = generate_synthetic_demographics_data()

# Preview the data to verify schema compliance and Euler grid alignment
print("Synthetic Demographic Data Preview (First 5 State Points):")
print(raw_demographics.head())


def load_study_configuration(filepath: str = "config.yaml") -> Dict[str, Any]:
    """
    Loads the study configuration parameters from a YAML file into a Python dictionary.

    Purpose:
        To ingest the deterministic hyperparameters, SDE coefficients, and forward 
        utility preferences defined in the external configuration file.

    Inputs:
        filepath (str): The path to the YAML configuration file. Default is "config.yaml".

    Outputs:
        Dict[str, Any]: A nested dictionary containing the study configuration.
    """
    if not isinstance(filepath, str):
        raise TypeError(f"filepath must be a string, got {type(filepath)}.")

    try:
        with open(filepath, "r", encoding="utf-8") as file:
            config = yaml.safe_load(file)
        print(f"\nSuccessfully loaded configuration from '{filepath}'.")
        return config
    except FileNotFoundError:
        print(f"\nCRITICAL ERROR: '{filepath}' not found. The pipeline requires this file.")
        raise
    except yaml.YAMLError as e:
        print(f"\nCRITICAL ERROR: Failed to parse YAML file '{filepath}': {e}")
        raise

# Load the configuration into memory
study_config = load_study_configuration("config.yaml")


# ==============================================================================
# Execution of the End-to-End Study Pipeline
# ==============================================================================

if __name__ == "__main__":
    # Ensure we have valid inputs before initiating the computationally heavy DAG
    if not raw_demographics.empty and study_config:
        
        print("\n" + "="*80)
        print("INITIATING MASTER ORCHESTRATOR: FUSED STATE-SPACE PIPELINE")
        print("="*80)
        
        try:
            # Execute the master orchestrator
            master_artifacts = execute_master_orchestrator(
                raw_demographics=raw_demographics,
                config=study_config
            )
            
            # ==============================================================================
            # Inspecting the Outputs and Verification Artifacts
            # ==============================================================================
            
            print("\n" + "="*80)
            print("STUDY EXECUTION COMPLETE: EXTRACTING ARTIFACTS")
            print("="*80)
            
            # 1. Accessing the Numerical Validation Report (Task 33)
            validation_report = master_artifacts["validation_report"]
            print("\n[Numerical Verification & Validation (V&V)]")
            print(f"Overall V&V Pass Status: {validation_report.overall_pass}")
            if validation_report.overall_pass:
                print("-> All stochastic processes and accounting identities hold perfectly.")
            else:
                print("-> WARNING: V&V failures detected. Review logs.")

            # 2. Accessing the Final Acceptance Report (Task 35)
            acceptance_report = master_artifacts["final_acceptance_report"]
            print("\n[Final Reproduction Acceptance Criteria]")
            print(f"Overall Reproduction Success: {acceptance_report.overall_reproduction_success}")
            print(f"Sustainability Finding: {acceptance_report.sustainability_acceptance.message}")
            print(f"Adequacy Finding: {acceptance_report.adequacy_acceptance.message}")
            print(f"Sensitivity Finding: {acceptance_report.sensitivity_acceptance.message}")

            # 3. Accessing the Generated Study Tables (Task 31)
            study_tables = master_artifacts["study_tables"]
            print("\n[Generated Artifact: EAIR Summary Table (First 5 Rows)]")
            print(study_tables.eair_table.head())

            # 4. Archiving Artifacts
            print("\n[Archiving]")
            print("To serialize tables to CSV and figures to PNG, call:")
            print("archive_research_artifacts(master_artifacts, output_dir='./reproduction_output')")

        except Exception as e:
            print(f"\nPIPELINE FAILED: An error occurred during orchestration: {e}")
            raise
            
    else:
        print("Error: Missing demographic data or configuration. Cannot proceed.")
```

## Output Structure

The pipeline returns a comprehensive dictionary containing nine key artifacts:
-   **`research_report`**: The immutable container holding the frozen environment, pathwise results, MC aggregates, and EAIR metrics.
-   **`depletion_integral_diagnostics`**: The validation of the theoretical hitting time invariant ($\tau = \tau^Z$).
-   **`demographic_comparison`**: The evaluation of SS vs. BB survival distributions.
-   **`sensitivity_report`**: The results of the $\delta$, $Z_0^u$, $F_0$, $\lambda$, $\omega_t$, and $\theta$ robustness checks.
-   **`study_tables`**: The formatted pandas DataFrames for EAIR, Depletion, and Adequacy summaries.
-   **`study_figures`**: The generated matplotlib Figure objects for market paths, policy paths, and MC distributions.
-   **`validation_report`**: The objective, boolean sign-off on the stochastic processes and accounting identities.
-   **`conventions_documentation`**: The formal record of manuscript baselines and numerical placeholder conventions.
-   **`final_acceptance_report`**: The definitive evaluation of the reproduction's fidelity to the paper's qualitative conclusions.

## Project Structure

```
optimal_investment_and_pension_policy_in_pay_as_you_go_systems/
│
├── optimal_investment_and_pension_policy_in_pay_as_you_go_systems_draft.ipynb  # Main implementation notebook
├── config.yaml                           # Master configuration file (SDEs & Preferences)
├── requirements.txt                      # Python package dependencies
│
├── LICENSE                               # MIT Project License File
└── README.md                             # This file
```

## Customization

The pipeline is highly customizable via the `config.yaml` file. Researchers can modify study parameters such as:
-   **Risk Aversion:** Adjust `theta_base` to evaluate how more conservative planners alter the optimal surplus distribution.
-   **Non-Hedgeable Risk Sensitivity:** Modify the `delta_vector` to test alternative state-contingent surplus rules (e.g., positive vs. negative wage sensitivity).
-   **Intergenerational Weighting:** Toggle `INTERGENERATIONAL_WEIGHTING` between `equal` and `cohort_weighted` to evaluate policies that explicitly protect larger cohorts.
-   **Initial Generosity:** Adjust the `initial_generosity_target_base` to observe the strict trade-off between immediate pension adequacy and long-term fund sustainability.

## Contributing

Contributions are welcome. Please fork the repository, create a feature branch, and submit a pull request with a clear description of your changes. Adherence to PEP 8, strict type hinting (`typing` module), and the 1:1 inline comment-to-code-line ratio is strictly required for all pull requests to maintain the implementation-grade standard of this repository.

## Recommended Extensions

Future extensions, building upon this foundational framework, could include:
-   **Stochastic Mortality Modeling:** Integrating models like Lee-Carter to endogenize demographic risk, moving beyond deterministic population trajectories.
-   **Multi-Asset Portfolios:** Expanding the financial market to include inflation-linked bonds or alternative assets, requiring a higher-dimensional Cholesky decomposition.
-   **Alternative Utility Kernels:** Implementing exponential or Epstein-Zin forward utilities to evaluate how different preference structures impact the optimal intergenerational risk-sharing mechanism.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Citation

If you use this code or the methodology in your research, please cite the original paper:

```bibtex
@article{alonsogarcia2026optimal,
  title={Optimal investment and Pension policy in Pay-As-You-Go systems under forward utility and ageing population},
  author={Alonso-Garcia, Jennifer and Hillairet, Caroline and Kaakai, Sarah and Mrad, Mohamed},
  journal={arXiv preprint arXiv:2605.12698},
  year={2026}
}
```

For the implementation itself, you may cite this repository:
```bibtex
@misc{chirinda2026pensionpolicy,
  author = {Chirinda, Craig},
  title = {Optimal Investment and Pension Policy in PAYG Systems: An Empirical Replication Pipeline},
  year = {2026},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/chirindaopensource/optimal_investment_and_pension_policy_in_pay_as_you_go_systems}}
}
```

## Acknowledgments

-   Credit to **Jennifer Alonso-Garcia**, **Caroline Hillairet**, **Sarah Kaakai**, and **Mohamed Mrad** for the foundational theoretical work and the derivation of the closed-form optimal control laws that form the entire basis for this computational replication.
-   This project is built upon the exceptional tools provided by the open-source community. Sincere thanks to the developers of the scientific Python ecosystem, particularly the **NumPy**, **Pandas**, **SciPy**, and **Matplotlib** contributors.

--

*This README was generated based on the structure and content of the `optimal_investment_and_pension_policy_in_pay_as_you_go_systems_draft.ipynb` notebook and follows best practices for research software documentation.*

