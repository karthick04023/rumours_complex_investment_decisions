# `README.md`

# A Qualitative Reasoning Engine for Rumour Impacts on Investment Decisions

<!-- PROJECT SHIELDS -->
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Python Version](https://img.shields.io/badge/python-3.9%2B-blue.svg)](https://www.python.org/downloads/)
[![Code style: black](https://img.shields.io/badge/code%20style-black-000000.svg)](https://github.com/psf/black)
[![Imports: isort](https://img.shields.io/badge/%20imports-isort-%231674b1?style=flat&labelColor=ef8336)](https://pycqa.github.io/isort/)
[![Type Checking: mypy](https://img.shields.io/badge/type_checking-mypy-blue)](http://mypy-lang.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-%23F37626.svg?style=flat&logo=Jupyter&logoColor=white)](https://jupyter.org/)
[![arXiv](https://img.shields.io/badge/arXiv-2509.00588-b31b1b.svg)](https://arxiv.org/abs/2509.00588)
[![Year](https://img.shields.io/badge/Year-2025-purple)](https://github.com/chirindaopensource/rumours_complex_investment_decisions)
[![Discipline](https://img.shields.io/badge/Discipline-Computational%20Finance%20%26%20AI-blue)](https://github.com/chirindaopensource/rumours_complex_investment_decisions)
[![Research](https://img.shields.io/badge/Research-Qualitative%20Reasoning-green)](https://github.com/chirindaopensource/rumours_complex_investment_decisions)
[![Methodology](https://img.shields.io/badge/Methodology-Constraint%20Programming-orange)](https://github.com/chirindaopensource/rumours_complex_investment_decisions)
[![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/numpy-%23013243.svg?style=flat&logo=numpy&logoColor=white)](https://numpy.org/)
[![SciPy](https://img.shields.io/badge/SciPy-%23025596?style=flat&logo=scipy&logoColor=white)](https://scipy.org/)
[![NetworkX](https://img.shields.io/badge/NetworkX-2A628F.svg?style=flat)](https://networkx.org/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c.svg?style=flat&logo=Matplotlib&logoColor=white)](https://matplotlib.org/)

--

**Repository:** `https://github.com/chirindaopensource/rumours_complex_investment_decisions`

**Owner:** 2025 Craig Chirinda (Open Source Projects)

This repository contains an **independent**, professional-grade Python implementation of the research methodology from the 2025 paper entitled **"Information-Nonintensive Models of Rumour Impacts on Complex Investment Decisions"** by:

*   Nina Bočková
*   Karel Doubravský
*   Barbora Volná
*   Mirko Dohnal

The project provides a complete, end-to-end computational framework that serves as a formal, auditable, and collaborative "reasoning engine" for exploring the complete set of possible future dynamics of a complex system. It delivers a modular and extensible pipeline that replicates the paper's entire workflow: from rigorous data validation and preprocessing, through the qualitative translation of system dynamics, to the formulation and solution of complex Constraint Satisfaction Problems (CSPs), and finally to the construction and analysis of a transitional graph that maps the entire state space of possible system behaviors.

## Table of Contents

- [Introduction](#introduction)
- [Theoretical Background](#theoretical-background)
- [Features](#features)
- [Methodology Implemented](#methodology-implemented)
- [Core Components (Notebook Structure)](#core-components-notebook-structure)
- [Key Callable: execute_full_project_pipeline](#key-callable-execute_full_project_pipeline)
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

## Introduction

This project provides a Python implementation of the methodologies presented in the 2025 paper "Information-Nonintensive Models of Rumour Impacts on Complex Investment Decisions." The core of this repository is the iPython Notebook `rumours_complex_investment_decisions_draft.ipynb`, which contains a comprehensive suite of functions to replicate the paper's findings, from initial data validation to the final generation of a strategic decision framework.

The paper addresses a critical challenge in finance and economics: how to model complex systems under severe information constraints where traditional quantitative models fail. This codebase operationalizes the paper's qualitative reasoning approach, allowing users to:
-   Rigorously validate and cleanse input financial data and correlation matrices.
-   Programmatically translate systems of differential equations (like a rumour-spreading model) into a parameter-free, qualitative format.
-   Formulate and solve complex Constraint Satisfaction Problems (CSPs) to derive all logically possible scenarios for a system's behavior.
-   Systematically resolve inconsistencies in data-driven models using a greedy heuristic algorithm.
-   Integrate multiple sub-models (e.g., a financial model and a social dynamics model) to study their emergent interactions.
-   Construct and analyze a "transitional graph" that represents the complete map of all possible dynamic pathways the system can follow over time.
-   Perform a multi-criteria decision analysis on the qualitative scenarios to derive actionable, strategic insights.

## Theoretical Background

The implemented methods are grounded in Artificial Intelligence (Qualitative Reasoning), Constraint Programming, and Financial Modeling.

**1. Qualitative State Representation (Trend Analysis):**
The core concept is the abstraction of a continuous variable's state into a qualitative "trend triplet": `(Value, DX, DDX)`. This captures the variable's sign (assumed positive, `+`), its first derivative (trend/velocity: `+`, `0`, `-`), and its second derivative (acceleration: `+`, `0`, `-`). A **scenario** is a complete snapshot of the system where every variable is assigned a trend triplet.

**2. Constraint Satisfaction Problem (CSP) Formulation:**
The dynamics of the system are not defined by numerical equations but by a set of logical constraints.
-   **Pairwise Influences:** Derived from data (e.g., correlation signs) or expert knowledge, these take the form of `SUP(X, Y)` (an increase in X supports an increase in Y) or `RED(X, Y)` (an increase in X reduces Y).
-   **Qualitative Algebraic Equations:** Derived from ODEs by eliminating parameters and applying qualitative arithmetic, e.g.:
    $$ \frac{dX}{dt} = -\alpha \frac{XY}{N} \quad \xrightarrow{\text{translation}} \quad DX + XY = 0 $$
The goal is to find all scenarios (assignments of triplets to variables) that simultaneously satisfy all constraints. This is a classic CSP.

**3. Transitional Graph:**
The set of all valid scenarios forms the nodes of a directed graph, `H = (S, T)`. An edge exists from scenario `S_i` to `S_j` if and only if the system can transition from state `S_i` to `S_j` in one time step, according to a set of predefined rules (from Table 2) that enforce continuity and smoothness. This graph represents the complete dynamic landscape of the model.

## Features

The provided iPython Notebook (`rumours_complex_investment_decisions_draft.ipynb`) implements the full research pipeline, including:

-   **Modular, Task-Based Architecture:** The entire pipeline is broken down into 29 distinct, modular tasks, from data validation to robustness analysis.
-   **Professional-Grade Data Validation:** A comprehensive validation suite ensures all inputs (data and configurations) conform to the required schema before execution.
-   **Auditable Data Preprocessing:** A non-destructive cleansing and preprocessing pipeline for both raw data and correlation matrices, returning a detailed log of all transformations.
-   **Custom Qualitative Reasoning Engine:** Implements a qualitative arithmetic engine and custom `Constraint` classes to translate algebraic qualitative equations into a solvable format.
-   **Systematic Inconsistency Resolution:** A faithful implementation of the paper's greedy heuristic algorithm to make over-constrained, data-driven models tractable.
-   **High-Fidelity Model Transcription:** Meticulous, programmatic transcription of all expert-defined models and rules from the paper's tables (Table 2, 4, 7) and equations (Eq. 11).
-   **Complete Graph Construction and Analysis:** Automated construction of the final transitional graph and a comprehensive analysis of its topological properties (partitions, cycles, etc.).
-   **Data-Driven Strategic Analysis:** A full suite of functions to perform multi-criteria scoring, ranking, and strategy evaluation on the final set of scenarios.
-   **Comprehensive Robustness Framework:** A master orchestrator to systematically test the sensitivity of the results to changes in parameters and alternative model specifications.

## Methodology Implemented

The core analytical steps directly implement the methodology from the paper:

1.  **Data and Configuration Validation (Tasks 1-3, 6):** Ingests and rigorously validates all raw data and the `config.yaml` file.
2.  **Data Preprocessing (Tasks 4-5):** Cleanses the raw data and preprocesses the correlation matrix for numerical stability.
3.  **CIM Construction (Tasks 7-9):** Derives an initial model from the correlation data, resolves inconsistencies, integrates expert knowledge, and solves for the 7 CIM scenarios.
4.  **RRM Construction (Tasks 10-12):** Translates the rumour-spreading ODEs into qualitative constraints and solves for the 211 RRM scenarios.
5.  **Model Integration (Tasks 13-14):** Merges the CIM and RRM, adds cross-model constraints, and solves for the final 14 integrated scenarios.
6.  **Dynamic Analysis (Tasks 15-18):** Analyzes the integrated scenarios, constructs the transitional graph, and validates its structure.
7.  **Decision Support and Reporting (Tasks 19-24):** Performs multi-criteria analysis, generates strategic recommendations, and creates final tables and visualizations.
8.  **Meta-Validation (Tasks 25-29):** Executes a final, exhaustive suite of correctness, reproducibility, and robustness checks on the entire pipeline and its results.

## Core Components (Notebook Structure)

The `rumours_complex_investment_decisions_draft.ipynb` notebook is structured as a logical pipeline with modular orchestrator functions for each of the major tasks. All functions are self-contained, fully documented, and designed for professional-grade execution.

## Key Callable: execute_full_project_pipeline

The central function in this project is `execute_full_project_pipeline`. It orchestrates the entire analytical workflow, providing a single entry point for running the baseline study replication and the advanced robustness checks.

```python
def execute_full_project_pipeline(
    raw_df: pd.DataFrame,
    correlation_matrix_df: pd.DataFrame,
    master_input_specification: Dict[str, Any]
) -> Dict[str, Any]:
    """
    Executes the entire end-to-end research pipeline and robustness analysis.
    """
    # ... (implementation is in the notebook)
```

## Prerequisites

-   Python 3.9+
-   Core dependencies: `pandas`, `numpy`, `scipy`, `networkx`, `matplotlib`, `pyyaml`, `python-constraint`.

## Installation

1.  **Clone the repository:**
    ```sh
    git clone https://github.com/chirindaopensource/rumours_complex_investment_decisions.git
    cd rumours_complex_investment_decisions
    ```

2.  **Create and activate a virtual environment (recommended):**
    ```sh
    python -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install Python dependencies:**
    ```sh
    pip install pandas numpy scipy networkx matplotlib pyyaml python-constraint
    ```

## Input Data Structure

The pipeline requires three inputs:
1.  **`raw_df`:** A `pandas.DataFrame` containing historical financial data for the 10 CIM variables.
2.  **`correlation_matrix_df`:** A 10x10 `pandas.DataFrame` with the Pearson correlation matrix for the CIM variables.
3.  **`master_input_specification`:** A Python dictionary loaded from the `config.yaml` file, which controls all aspects of the pipeline.

A mock data generation code block is provided in the main notebook to create valid example DataFrames for testing the pipeline.

## Usage

The `rumours_complex_investment_decisions_draft.ipynb` notebook provides a complete, step-by-step guide. The core workflow is:

1.  **Prepare Inputs:** Load or generate the `raw_df` and `correlation_matrix_df`. Load the configuration from `config.yaml`.
2.  **Execute Pipeline:** Call the grand master orchestrator function.

    ```python
    # This single call runs the entire project.
    final_project_report = execute_full_project_pipeline(
        raw_df=raw_df,
        correlation_matrix_df=correlation_matrix_df,
        master_input_specification=master_input_specification
    )
    ```
3.  **Inspect Outputs:** Programmatically access any result from the returned dictionary. For example, to view the final strategic decision framework:
    ```python
    decision_framework = final_project_report['baseline_pipeline_report']['task_reports']['task_21_strategy_report']['outputs']['decision_framework']
    print(decision_framework)
    ```

## Output Structure

The `execute_full_project_pipeline` function returns a single, comprehensive dictionary containing all generated artifacts, including:
-   `baseline_pipeline_report`: A dictionary containing the detailed reports from every task in the main pipeline run, including the final scenario lists, the transitional graph object, and the strategic analysis.
-   `robustness_analysis_report`: A dictionary containing the summary DataFrames from each of the executed robustness and sensitivity checks.

## Project Structure

```
rumours_complex_investment_decisions/
│
├── rumours_complex_investment_decisions_draft.ipynb   # Main implementation notebook
├── config.yaml                                        # Master configuration file
├── requirements.txt                                   # Python package dependencies
├── LICENSE                                            # MIT license file
└── README.md                                          # This documentation file
```

## Customization

The pipeline is highly customizable via the `config.yaml` file. Users can easily modify all relevant parameters, such as CSP solver settings, inconsistency removal limits, and the definitions of expert knowledge, without altering the core Python code.

## Contributing

Contributions are welcome. Please fork the repository, create a feature branch, and submit a pull request with a clear description of your changes. Adherence to PEP 8, type hinting, and comprehensive docstrings is required.

## Recommended Extensions

Future extensions could include:

-   **Automated Report Generation:** Creating a function that takes the final `master_report` dictionary and generates a full PDF or HTML report summarizing the findings.
-   **Generalization:** Refactoring the code to handle arbitrary model definitions (variables and constraints) specified entirely within the `config.yaml` file, turning it into a general-purpose qualitative reasoning engine.
-   **Alternative Solvers:** Integrating more powerful CSP solvers like Google's OR-Tools to handle larger and more complex models.
-   **Policy Experiments:** Adding new expert constraints to the integrated model to simulate the impact of policy interventions (e.g., a public information campaign to counter a rumour) and observing how the transitional graph changes.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Citation

If you use this code or the methodology in your research, please cite the original paper:

```bibtex
@article{bockova2025information,
  title={{Information-Nonintensive Models of Rumour Impacts on Complex Investment Decisions}},
  author={Bo{\v{c}}kov{\'a}, Nina and Doubravsk{\'y}, Karel and Voln{\'a}, Barbora and Dohnal, Mirko},
  journal={arXiv preprint arXiv:2509.00588},
  year={2025}
}
```

For the implementation itself, you may cite this repository:
```
Chirinda, C. (2025). A Qualitative Reasoning Engine for Rumour Impacts on Investment Decisions.
GitHub repository: https://github.com/chirindaopensource/rumours_complex_investment_decisions
```

## Acknowledgments

-   Credit to **Nina Bočková, Karel Doubravský, Barbora Volná, and Mirko Dohnal** for their innovative research, which forms the entire basis for this computational replication.
-   This project is built upon the exceptional tools provided by the open-source community. Sincere thanks to the developers of the scientific Python ecosystem, including **Pandas, NumPy, SciPy, NetworkX, Matplotlib**, and the **python-constraint** library, whose work makes complex computational science accessible and robust.

--

*This README was generated based on the structure and content of `rumours_complex_investment_decisions_draft.ipynb` and follows best practices for research software documentation.*

