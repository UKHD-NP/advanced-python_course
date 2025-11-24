# Repository Guidelines
Package name: `Advanced python course`

This document defines the aims, purpose and schedule of the course, as well as the repository structure and conventions. It serves as a reference for developers and LLM-based assistants to understand the context, maintain consistency and quality while building or modifying the repository.

---

## Overview

This repository hosts an advanced python course. The course focuses on teaching how to write reproducible and documented functions, structure them into a minimal python package and perform version control as well as collaborative working with git and github. To this aim, the students perform a simulated proteomics experiment using python while learning about bottom-up mass spectrometry based proteomics. The mass-spectrometry experiment simulation is performed by a sequence three jupyter notebooks `protein_digestion.ipynb`, `liquid_chromatography.ipynb` and `mass_spectra_simulation.ipynb` which recreate the main steps of a proteomics pipeline. These tutorials are intended to be processed by the student one per day and capture the three major concepts in mass spectrometry proteomics.

As a reference for how the package that the students will develop should look like, a softlink to a model package is included within the current repository. The aim is for the students to create a package with identical function names as well as identical input and outputs. You will use this repository as reference when designing the course, creating tutorial instructions and writing code for the tutorials. For example you will use the proteosim/tutorials/ms_simulation.ipynb to create the backbone of the final notebook that the students will create and where they will use the functions they created in their version of the proteomics package. The final aim for the student is to be able to create and run a proteomics in-silico experiment within a short jupyter notebook, as in the proteosim/tutorials/ms_simulation.ipynb.


## Python knowledge prerequisites

- String operations
- Regular expressions
- Lists and dictionaries
- List and dictionary comprehensions
- Slicing
- Loops
- If/else statements
- Using external libraries
- NumPy
- Pandas
- Simple visualizations with Matplotlib
- Function writing
- Theoretical introduction into python function writing, unit tests, package development practices and version control


## Learning goals

- Reproducible function writing
- Package and function documentation
- Unit testing
- Version control with git
- Package publication with Github
- Collaborative coding with git and Github


## Schedule

The course is divided into five days of practical exercises. During the first three days, the students complete the three tutorial notebooks, which are oriented to create a set of essential functions and respective unit tests which will become part of the minimal python package. On the fourth day the students copy these essential functions and tests from the respective notebooks and insert them into the minimal package that they are developing and to commit their additions.
- Day 1 (Monday):
    - complete tutorial 1: `1_peptide_digestion.ipynb` including essential functions for the minimal package
    - add tests for the new functions
- Day 2 (Tuesday):
    - complete tutorial 2: `2_liquid_chromatography.ipynb` including essential functions for the minimal package
    - add tests for the new functions
- Day 3 (Wednesday):
    - complete tutorial 3: `3_mass_spectra_simulation.ipynb` including essential functions for the minimal package
    - add tests for the new functions
- Day 4 (Thursday):
    - complete tutorial 4: `4_build_your_own_package.md` including essential functions for the minimal package
    - create python package backbone: code directory, init files and pyproject.toml
    - install the package in editable mode using pip
    - create the final jupyter notebook where they directly apply the package they developed to perform a streamlined proteomics experiment from reading the protein fasta file to generating the mass-spectra of the digested peptides and a the mass-spectra of the chosen "MATSR" peptide fragments. A backbone will be provided for this.
- Day 5 (Friday):
    - complete tutorial 5: `5_publish_your_package.md` including essential functions for the minimal package
    - Prepare package for upload by adding README.md file and adding package
      documentation.
    - upload the package repository to Github
    - download the package of a peer, execute the final notebook with the peer's functions and same fasta file as input and compare the following output files:
        - digested_peptides_mz.tsv
        - <selected_peptide>_fragments_mz.tsv

See the proteosim repository for details about the mass spectrometry experiment simulation. In short, a protein fast is read, the protein sequences are split based on the cleavage pattern of a specific protease such as trypsin and the peptides are pooled. Then the retention times of the liquid_chromatography are predicted for each peptide. Next, a retention time window is selected for which the mass-charge ratio of the peptides are computed (added charge = 2). Finally, the "MATSR" peptide is selected and fragment ions are computed. Finally, the mass-charge ratio of the fragment ions is calculated (charge = 1)

The essential functions which the students will write, create tests for and
then copy and paste to their minimal package are: 

- fasta file handling: `read_fasta`
- protein digestion: `digest_protein_sequence`, `digest_protein_collection`, `compute_sequence_coverage` and the variable `enzyme_cleavage_patterns`
- liquid chromatography: `predict_lc_retention_times`, `plot_retention_time`
- mass spectrometry simulation: `select_retention_time_window`, `calculate_mol_mass`, `calculate_mol_mass_collection`, `calculate_mz`, `calculate_mz_collection`, `plot_spectrum`, `fragment_peptide`, plus the variable `amino_acid_mass_dalton`

See proteosim repository for details. As a side-note, the modules file_handling and peptide_digestion are both covered in tutorial 1: `peptide_digestion.ipynb` of the present repository.

## File and directory structure
The course root resides under `advanced-python_course/`. The main tutorial notebooks are located directly under root. Sub-directories are organized by functionality:

```
advaned-python_course/
├── results/      # Proteomics experiment output
├── README.md
├── data/         # Includes input protein fasta file
├── proteosim/    # Softlink to model repository. Only for view of the LLM or creator of the course repository.
├── templates/    # E.g. pyproject.toml
└── tutorials/
     ├── 1_protein_digestion.ipynb
     ├── 2_liquid_chromatography.ipynb
     ├── 3_mass_spectra_simulation.ipynb
     ├── 4_build_your_own_package.ipynb
     └── 5_publish_your_package.ipynb
```


## Tutorial guidelines
The mass spectrometry simulation tutorial notebooks use a combination of markdown and code. Markdown cells preface code cells and include instructions, context, and explanations about the biology of the simulation that is being performed. The instructions are designed so that the student learns about the biology while creating a set of essential functions which will be afterwards collected and inserted into the package that they are developing (see proteosim reference repository to know which essential functions are to be written for the package). For the essential functions such as `read_fasta`, `digest_protein_sequence`, `predict_lc_retention_times` etc provide an empty function backbone as such:

```python
def essential_function(predefined_args):
    """
    Describe function

    Parameters
    ----------

    Returns
    -------
    """
    pass
```

For the essential functions (see proteosim reference repository), the tutorial will also guide the student to create simple testing functions without fixtures so that they can easily be copied over to the minimal package that is being developed. The student should also be guided by the type of input and output that the test function should use.


## Coding style
follow Pep8 and numpy/scipy docstring conventions.


## Main tutorial components of the repository

- README.md: short introduction, requirements and references to the tutorials, which
  the students should perform in order 1 to 5.
- tutorials: 1 to 5.
- templates: contains a few blueprints such as the pyproject.toml and the final notebook backbone.
- data: contains the input fasta file
**End of AGENTS.md**




















# AGENTS.md — Advanced Python Course Repository Specification

## Purpose

This document defines **the aims, structure, and conventions** of the `advanced-python_course` repository.  
It is designed to help both **human developers** and **LLM-based assistants** (such as ChatGPT) understand the repository’s content, dependencies, and workflow — ensuring **consistent behavior, coherent course generation, and reproducible results**.

LLMs should use this document as a **context guide** when:
- Generating or editing course materials (e.g., tutorials, notebooks, templates)
- Writing Python code examples and tests
- Assisting in course design, structure, and automation

---

## 1. Repository Overview

The `advanced-python_course` repository hosts a **five-day intensive training course** on advanced Python for scientific programming and reproducible research.

### Course Theme
Students simulate a **mass spectrometry-based proteomics experiment** using Python.  
They will:
1. Implement modular functions with clear documentation and testing.
2. Combine these functions into a minimal Python package.
3. Manage version control and collaboration through Git and GitHub.

### Simulation Pipeline
The experiment is divided into **three core simulation stages**, each represented by a Jupyter notebook:

| Stage | Notebook | Concept |
|--------|-----------|----------|
| 1. Protein Digestion | `1_protein_digestion.ipynb` | Protease-based cleavage of protein sequences |
| 2. Liquid Chromatography | `2_liquid_chromatography.ipynb` | Retention time prediction |
| 3. Mass Spectra Simulation | `3_mass_spectra_simulation.ipynb` | Fragmentation and ion mass calculation |

These notebooks parallel the biological workflow of bottom-up proteomics.

---

## 2. Reference Package

A **model repository** (`proteosim/`) is provided as a **softlink** for the instructor or LLM reference.  
It defines:
- **Expected function names**
- **Required input/output formats**
- **Intended functional behavior**

LLMs should:
- Use `proteosim/tutorials/ms_simulation.ipynb` as the canonical example for the final integrated notebook.
- Preserve naming, signatures, and docstring structures in any generated functions or tests.

**Goal:** Students will replicate this pipeline in their own minimal package and execute it to reproduce the final experiment results.

---

## 3. Prerequisites

### Python Skills
Students must be familiar with:

- Core data types: strings, lists, dicts, slicing, comprehensions  
- Control structures: loops, if/else  
- Regex and string parsing  
- External library usage (NumPy, Pandas, Matplotlib)  
- Function definitions and docstrings  
- Unit testing principles  
- Basics of version control (Git)

### Conceptual Skills
- Writing reproducible, testable functions  
- Structuring small Python packages  
- Documenting code with docstrings (NumPy/SciPy format)  
- Managing collaborative repositories via GitHub

---

## 4. Learning Objectives

By the end of the course, students should be able to:

- Write **documented, reproducible** Python functions  
- Create and test functions modularly  
- Organize code into a distributable package  
- Use **Git/GitHub** for version control and collaboration  
- Publish and evaluate peer-developed packages

---

## 5. Course Schedule

The course is structured as a **five-day progressive workshop**:

| Day | Focus | Deliverables |
|-----|--------|--------------|
| **1 (Mon)** | Protein digestion functions (`1_protein_digestion.ipynb`) | Implement digestion + tests |
| **2 (Tue)** | Liquid chromatography (`2_liquid_chromatography.ipynb`) | Implement LC functions + tests |
| **3 (Wed)** | Mass spectra simulation (`3_mass_spectra_simulation.ipynb`) | Implement MS functions + tests |
| **4 (Thu)** | Package assembly (`4_build_your_own_package.ipynb`) | Build Python package; integrate prior work |
| **5 (Fri)** | Package publication (`5_publish_your_package.ipynb`) | Push to GitHub; peer-test results |

### Final Experiment
Students will:
1. Run their package end-to-end on a provided FASTA file.  
2. Generate:
   - `digested_peptides_mz.tsv`  
   - `<selected_peptide>_fragments_mz.tsv`
3. Compare their results with a peer’s package outputs.

---

## 6. Essential Functions (to be implemented by students)

Each tutorial produces functions that will later be integrated into a minimal package.  
LLMs generating code must maintain these **exact names and parameters**.

### File Handling
- `read_fasta`

### Protein Digestion
- `digest_protein_sequence`
- `digest_protein_collection`
- `compute_sequence_coverage`
- Variable: `enzyme_cleavage_patterns`

### Liquid Chromatography
- `predict_lc_retention_times`
- `plot_retention_time`

### Mass Spectrometry
- `select_retention_time_window`
- `calculate_mol_mass`
- `calculate_mol_mass_collection`
- `calculate_mz`
- `calculate_mz_collection`
- `plot_spectrum`
- `fragment_peptide`
- Variable: `amino_acid_mass_dalton`

---

## 7. Repository Structure
advanced-python_course/
├── README.md
├── data/ # Input FASTA files
├── results/ # Student-generated outputs
├── proteosim/ # Reference softlink (read-only for students)
├── templates/ # Blueprints (e.g., pyproject.toml)
├── tutorials/ # Core teaching notebooks
│ ├── 1_protein_digestion.ipynb
│ ├── 2_liquid_chromatography.ipynb
│ ├── 3_mass_spectra_simulation.ipynb
│ ├── 4_build_your_own_package.ipynb
│ └── 5_publish_your_package.ipynb
└── results/ # Output comparison files


---

## 8. Tutorial Design Guidelines

Each notebook combines:
- **Markdown cells**: Explain biological and computational concepts. Keep expressions simple and language more biology focused rather than computer science. The target audience are molecular biotechnology students specializing in bioinformatics and learning to code. Focus on explaining why the concepts they are learning are useful by showing the relationship to bioinformatics.
- **Code cells**: Contain partial implementations or placeholders for essential functions.
In addition, try not to rely on external libraries except for scientific ones such as pandas, numpy and sci-kit learn. Avoid using non-essential libraries such as pathlib and collections.

Example template for essential functions:

```python
def essential_function(predefined_args):
    """
    Short description of what the function does.

    Parameters
    ----------
    param_name : type
        Description.

    Returns
    -------
    return_type
        Description.
    """
    pass


LLMs should:

- Keep function names identical to the reference package.
- Write minimal, readable code aligned with course goals (clarity > efficiency).
- Ensure all functions have unit tests without using complex test fixtures.


---

## 9. Coding Standards

- PEP8 compliance
- NumPy/SciPy docstring conventions
- Meaningful variable and function names
- Clear comments for pedagogical clarity
- Modular design: each function must have one clear responsibility


---

## 10. Core Repository Components

| File         | Description                                       |
| ------------ | ------------------------------------------------- |
| `README.md`  | High-level overview and course workflow           |
| `tutorials/` | Step-by-step exercises (Days 1–5)                 |
| `templates/` | Ready-to-use boilerplates (e.g. `pyproject.toml`) |
| `data/`      | Input FASTA datasets                              |
| `proteosim/` | Instructor-only model repository                  |
| `results/`   | Experiment outputs                                |


---

### 11. LLM-Specific Instructions

To maximize alignment and output quality:
1. **Prioritize pedagogical clarity** over optimization.
2. Reference the `proteosim` package for expected behaviors.
3. When writing or modifying code:
- Include complete docstrings.
- Write assert-based tests.
- Comment with short instructional cues (e.g., # Student: replace pass with your code).
4. When generating notebooks or text, maintain consistent ordering and naming.
5. Avoid importing unavailable or external non-standard libraries.
6. When referencing files or functions, assume the working directory is the repository root.


---

12. Summary

This repository provides the foundation for a structured, reproducible, and biologically contextual **advanced Python training**.
All generated or edited materials — whether by instructors or LLMs — must preserve:
- Reproducibility
- Pedagogical clarity
- Functional consistency
- Alignment with the reference proteosim package
**Beginning of AGENTS.md**
