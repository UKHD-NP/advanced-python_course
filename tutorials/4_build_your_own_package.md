# Tutorial 4 – Build Your Own Proteomics Package

> 🤖 **AI co-pilot reminder:** Modern LLMs like ChatGPT-5 have been trained on thousands of Python packages and are surprisingly good at guiding packaging tasks. Feel free to ask an LLM to explain steps, draft templates, or suggest improvements as you work.

This tutorial guides you through turning the functions from Tutorials 1–3 into a minimal Python package, installing it, running unit tests, and using it inside the final proteomics notebook. We will go step by step so you can transform research code into a reusable tool.

> 🧩 **Tipp**
> 
> Try to perform this tutorial by yourself first. If you get stuck at any point, feel free to check out a complete reference repository at https://github.com/UKHD-NP/proteosim/tree/main.

---

## 1. Create the minimal package structure
A Python package needs a standard layout so that pip, imports, and test tools know where everything lives. It consists of:
- A `pyproject.toml` that describes metadata and dependencies.
- A source directory named after your package (e.g., `proteosim/`) with `__init__.py` files.
- A `tests/` directory mirroring the source layout.

`__init__.py` files tell Python that a directory should be treated as a module (so `import proteosim` works). They can be empty, but every package directory—including `tests/`—needs one. If you want certain functions to be part of the public API (e.g., `from proteosim import read_fasta`), import them in `proteosim/__init__.py` so users get a clean entry point.

Follow these steps:
1. **Create a project folder** (e.g., `proteosim/`) if you have not done so already.
2. **Copy the template `pyproject.toml`** from `[templates/pyproject.toml](templates/pyproject.toml)` into the project root and edit:
   - `[project] name` (e.g., `proteosim`).
   - `version` (start at `0.1.0`).
   - `description`, `readme`, `authors`, and `dependencies` (include `pyteomics`, `numpy`, `matplotlib`).
3. **Create the source module directory** (matching your package name):
   ```
   proteosim/
   ├── proteosim/
   │   ├── __init__.py
   │   ├── file_handling.py
   │   ├── protein_digestion.py
   │   ├── liquid_chromatography.py
   │   └── simulate_mass_spectra.py
   └── tests/
       ├── __init__.py
       ├── test_file_handling.py
       ├── test_protein_digestion.py
       ├── test_liquid_chromatography.py
       └── test_simulate_mass_spectra.py
   ```
4. **Add `__init__.py` files** to the package directory and to each sub-package (if any) so Python treats the directories as modules.
5. **Create matching test files** under `tests/`, using the same module names (prefixed with `test_`).
6. **Copy your functions** from Tutorials 1–3 into the corresponding module files, import the public ones in `proteosim/__init__.py`, and copy the assert-based unit tests into the matching `test_*.py` files. You can also save variables in the modules: e.g. `enzyme_cleavage_patterns` and `amino_acid_mass_dalton`. Hint: ⭐ essential function and ✅ test function.

Once this structure is in place, you are ready to install the package in editable mode and run the test suite. 🚀

## 2. Install the package in editable mode
Once your package structure is in place, install it locally so you can import it from anywhere.

1. From inside the project root (next to `pyproject.toml`), run:
   ```bash
   pip install -e .
   ```
   The `-e/--editable` flag links your working directory into the Python environment, so code changes take effect immediately without reinstalling.
2. Verify the install by opening a Python shell (or notebook) and importing your package:
   ```python
   import proteosim as ps
   proteins = ps.read_fasta('data/sample_proteins.fasta')
   len(proteins)
   ```
3. If the import fails, double-check that the package name in `pyproject.toml` matches the source directory name and that you activated the correct virtual environment.


## 3. Run the full pipeline via your package
With Tutorials 1–3 wrapped into a package, you can reproduce the entire proteomics workflow with a handful of function calls.
Use the template backbone as guidance `[tutorials/ms_simulation_final.ipynb](tutorials/ms_simulation_final.ipynb)` and fill in the code cells with your package functions.


For example:
```python
import proteosim as ps

proteins = ps.read_fasta('data/sample_proteins.fasta')
```

## 4. Run pytest to validate the package
Testing protects your workflows from silent regressions. Once your code and tests are in place:

1. From the project root (next to `pyproject.toml`), execute:
   ```bash
   pytest
   ```
   or target specific files with `pytest tests/test_file_handling.py`.
2. Fix any failing tests before moving on. They often reveal import issues, missing `__init__.py` files, or mismatched function signatures.
3. Re-run `pytest` until the suite passes green. Keep doing this after every significant change.

A clean test run confirms that the package you install and publish behaves exactly like the notebooks you developed earlier.


## 5. (Optional) Practice a mini Git workflow
If you'd like to rehearse a Git flow, try this lightweight exercise:

1. `git init` inside your package directory.
2. `git add pyproject.toml && git commit -m "Add project metadata"`
3. `git add proteosim/ && git commit -m "Add core package modules"`
4. Create a branch for tests: `git checkout -b tests`
5. `git add tests/ && git commit -m "Add unit tests"`
6. Switch back to main: `git checkout main`
7. Merge the tests branch: `git merge tests`
8. Remove old branch: `git branch -d tests`

This fake workflow mirrors how you might collaborate on GitHub without needing a remote repository.
