# Tutorial 6 – Build and Publish Your Proteomics Package

> 🤖 **AI co-pilot reminder:** Modern LLMs like ChatGPT-5 have been trained on thousands of Python packages and are surprisingly good at guiding packaging tasks. Feel free to ask an LLM to explain steps, draft templates, or suggest improvements as you work.

This tutorial guides you through turning the functions from Tutorials 1–3 into a minimal Python package, installing it, running unit tests, practicing typical Git workflows, and publishing the finished project on GitHub. We will go step by step so you can transform research code into a reusable tool and keep every change tracked from the very first commit. Make sure you have a GitHub account available, since we will push to a remote repository as part of the workflow.


> 🧩 **Tipp**
>
> Try to perform this tutorial by yourself first. If you get stuck at any point, feel free to check out a complete reference repository at https://github.com/UKHD-NP/proteosim/tree/main.

---

## 1. Create and clone a GitHub repository
Start online so that every local change can be pushed immediately:

1. Log into GitHub and click **New repository**.
2. Enter a short, descriptive name (e.g. proteosim), set the visibility to public, and tick the boxes to create a `README.md` and select an open-source license (MIT or Apache 2.0 both work well). In the present tutorial we will refer to your package name as `proteosim`)
3. After the repository is created, copy the HTTPS URL and clone it locally:
   ```bash
   git clone https://github.com/<user>/proteosim.git
   cd proteosim
   ```
4. Verify that the `origin` remote points to your GitHub repository:
   ```bash
   git remote -v
   ```
   The remote is the online location where `git push` sends your commits, so double-check it matches your GitHub URL before continuing.

You now have a fresh local copy of the repository you initialized on GitHub that already contains placeholder `README.md` and `LICENSE` files. We will keep reshaping this repository and pushing updates throughout the tutorial. Because you cloned it, the folder is already under Git version control—`ls -a` will show the hidden `.git/` directory that tracks every commit.

## 2. Verify Git tracking (or initialize it)
Because you cloned from GitHub, the repository already contains the hidden `.git/` directory. Confirm that Git is active by running `git status` inside the project root; you should see a clean working tree with the files that GitHub created online. If you skipped the cloning step and created the folder locally, run `git init` now to start tracking changes before proceeding.

## 3. Create an initial README
`README.md` is the landing page for anyone visiting your repository. It should answer three questions:
- What does this project do?
- What are the requirements or installation steps?
- How can someone use it?

> ℹ️ Since you created your repository directly from Github, you will probably already have a `README.md` template file created automatically under the root of your repository.

You will keep improving the README as the package matures, but for now edit the placeholder file so GitHub has something meaningful to display after the first push. Add a title (e.g., `# Proteosim Course Package`) followed by three short sentences describing the purpose of the repository, the proteomics simulation focus, and the fact that the code is under active development.

Once the file is saved, stage it and create your first commit:

```bash
git add README.md
git commit -m "Add initial README"
```

Push the commit to GitHub:

```bash
git push -u origin main
```

Finally, run `git log` to verify that the commit appears in your history. This early push gives you a backup from the very beginning and lets you watch your repository evolve as you add more files.

## 4. Add a minimal `pyproject.toml`
`pyproject.toml` is the standardized configuration file for Python projects. Build tools such as `pip` read it to discover your package name, version, dependencies, and build backend. Without it, `pip install .` will fail, so add one early and keep it updated as the project grows.

1. Copy the course template `templates/pyproject.toml` file into your repository root.
2. Open the file and edit the `[project]` section:
   - `name`: match your package folder name (e.g., `proteosim`).
   - `version`: start at `0.1.0`.
   - `description`/`readme`: reuse the short description from your README.
   - `authors`: add your name and email.
   - `dependencies`: at minimum include `numpy`, `pandas`, `matplotlib` and `pyteomics`; you can expand this list later if needed.
3. Under [tool.setuptools.packages.find] update your package name as well.

After saving, run `git status` to confirm the new file is tracked, then `git add pyproject.toml` followed by `git commit -m "Add pyproject configuration"`. Push the commit so the remote stays in sync with your local progress. You will be able to see the file now in your Github repository webpage.

## 5. Create code and test modules
Now scaffold the directories that will hold your package code and tests. Aim for the following structure:

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

Create the directories and empty files. You can do this quickly from the terminal:
```bash
mkdir -p proteosim tests
touch proteosim/__init__.py tests/__init__.py
touch proteosim/file_handling.py proteosim/protein_digestion.py proteosim/liquid_chromatography.py proteosim/simulate_mass_spectra.py
touch tests/test_file_handling.py tests/test_protein_digestion.py tests/test_liquid_chromatography.py tests/test_simulate_mass_spectra.py
```
If you prefer a graphical approach, create the folders and empty files manually using your file manager, mirroring the same naming scheme.

Your code will reside under the main code directory `<proteosim>` (also named source directory). `__init__.py` files tell Python that a directory should be treated as a module (so `import proteosim` works). They can be empty, but every package directory—including `tests/`—needs one. If you want certain functions to be part of the public API (e.g., `from proteosim import read_fasta`), import them in `proteosim/__init__.py` so users get a clean entry point.

The `tests/` directory mirrors the modules in `proteosim/` with filenames prefixed by `test_`. This convention helps Pytest discover the right test suite automatically (`tests/test_file_handling.py` contains tests for `proteosim/file_handling.py`) and keeps your code and tests organized one-to-one.

Once the skeleton is in place, stage and commit the new directories with a descriptive commit message.

Your repository now has a clear layout ready for the functions and tests you will migrate from Tutorials 1–3.

## 6. Install the package in editable mode
Before you start filling the module files with real code, install the package locally in editable (a.k.a. development) mode. Editable installs enables dynamic use of the package without having to install it again after every change. In other words, `import proteosim` always loads the package with the latest changes. Make sure to perform this installation in your project-specific environment.

From the project root (next to `pyproject.toml`) activate your course virtual environment and run:

```bash
pip install -e .
```

The `-e` flag keeps pip pointing at your source directory. Any changes to files in `proteosim/` are immediately available to notebooks or scripts without reinstalling. You can verify the install inside a Python shell:

```python
import proteosim as ps
print(ps.__file__)
```

The path should resolve to the `proteosim` folder inside your repository.

## 7. First module `file_handling` and actions setup
From this point onward you will iterate through each module, copying the ⭐ essential functions from the notebooks into the package, validating them in a dedicated notebook, and then copying the matching ✅ tests. Start by creating a working notebook that will become your final proteomics experiment script:

1. In the repository root (outside the `proteosim/` package directory), create a blank `ms_experiment_final.ipynb`.
2. This notebook serves two purposes:
   - Quickly verify that the functions you move into the package behave as expected (`import proteosim as ps` and call the new function).
   - Assemble the final streamlined proteomics workflow you will later share with your peers.

Move the first essential function:

1. Open `proteosim/file_handling.py` and paste the ⭐ `read_fasta` implementation from Tutorial 1. Keep the NumPy-style docstring intact so the package remains well documented.
2. Save the file and switch to `ms_experiment_final.ipynb`. Import your package and call the function to make sure it can read the FASTA file:
   ```python
   import proteosim as ps
   proteins = ps.read_fasta("data/sample_proteins.fasta")
   len(proteins)
   ```
   Running this notebook cell confirms that the editable install updates immediately.
3. Copy the ✅ test for `read_fasta` into `tests/test_file_handling.py`, rename the function name by adding a "test_" prefix to "test_read_fasta". Following the `test_*` naming convetion for test functions is important as it allows the testing tool `pytest` to find the correct functions to test.

4. Run the test workflow from your repository root:
   ```bash
   pytest -v tests
   ```
   Fix any import paths or assertion errors before continuing. If pytest reports failures, resolve them immediately and re-run the suite until everything passes—never commit code with broken tests.
5. Commit and push the changes:
   ```bash
   git add proteosim/file_handling.py tests/test_file_handling.py ms_experiment_final.ipynb
   git commit -m "Add file_handling.py implementation and tests"
   git push
   ```

6. Set up automated testing with GitHub Actions:
   - A GitHub Actions workflow runs predefined tasks (jobs) on GitHub’s servers whenever certain events happen in your repository (pushes, pull requests, scheduled runs). Our goal is to automatically execute `pytest` so you catch bugs directly on the Github interface too.
   - Create a workflow file `proteosim/.github/workflows/tests.yml` that installs Python, sets up dependencies, and runs `pytest` on the trigger events: push to `main`/`master` and create pull request. Github will automatically detect this file and run the action.
   - If you have access to a powerful LLM such as ChatGPT-5, let it draft the workflow for you — it has been trained on thousands of Github actions files. For example, you can prompt:
     ```
     Create a GitHub Actions workflow called "tests" for a Python project that uses pyproject.toml.
     It should run on ubuntu-latest, set up Python 3.10, install dependencies with pip, and execute pytest. My dependecies are <your python dependences>.
     Trigger it on push or pull_request events targeting main or master.
     ```
   - Paste the generated YAML formated text into `.github/workflows/tests.yml`, commit it, and push. GitHub will automatically run the workflow on your next push; check the “Actions” tab or the ✅/❌ symbol next to your commit to confirm it passes.

You will repeat the same workflow described in the numbered steps above (1-5) for every module in the package.

## 8. Module `protein_digestion`
Next, add the functions that allow you to perform the protein digestion steps.

1. In `proteosim/protein_digestion.py`, paste the ⭐ essential functions from Tutorial 1: `digest_protein_sequence`, `digest_protein_collection`, and `compute_sequence_coverage`. Optionally also save the variable `enzyme_cleavage_patterns` if you want to be able to access protease cleave patterns directly using your package.
2. In `ms_experiment_final.ipynb`, extend your workflow to:
   - Digest the protein sequence dictionary with `ps.digest_protein_collection` with a protease of your choice.
   - Calculate sequence coverage for a selected protein using `compute_sequence_coverage`.
3. Copy the corresponding ✅ tests into `tests/test_protein_digestion.py`, keeping the `test_*` naming style.
4. Execute `pytest -v tests/test_protein_digestion.py` (or `pytest -v tests`) and fix any issues before moving on.
5. Commit and push the updated module, tests, and notebook changes.
6. Check the GitHub Actions tab to ensure the automated tests run successfully for this push.

## 9. Module `liquid_chromatography`
Follow the same numbered workflow steps 1-5 as before, but this time focus on the chromatography logic:

1. In `proteosim/liquid_chromatography.py`, paste the ⭐ essential functions `predict_lc_retention_times`, `plot_retention_time` and `select_retention_time_window` from Tutorial 2, including their docstrings.
2. Use `ms_experiment_final.ipynb` to validate the new functionality and to continue building your final experiment notebook: after digesting proteins, use your functions to predict the relative retention times for the pooled peptides, plot the chromatographic profile and to select a retention-time window of interest.
3. [...]

## 10. Module `simulate_mass_spectra`
Finish by migrating the mass spectrometry functions:

1. In `proteosim/simulate_mass_spectra.py`, paste the ⭐ essentials from Tutorial 3: `calculate_mol_mass`, `calculate_mol_mass_collection`, `calculate_mz`, `calculate_mz_collection`, `plot_ms`, and `fragment_peptide`. Also save your `amino_acid_mass_dalton` dictionary here so you can easily access it from your package.
2. Extend `ms_experiment_final.ipynb` so that it performs the complete mass-spectrometry proteomics simulation: filter peptides using the retention-time window, compute masses/mz values, plot the MS1 spectrum, fragment the MATSR peptide to produce the fragment-ions and plot the MS2 spectrum.
3. [...]

## 11. Lock dependencies and enrich the README
With the core modules ready, finalize the environment and documentation so others can run your package without guesswork:

1. Freeze your exact Python dependencies into `requirements.txt`:
   ```bash
   pip freeze > requirements.txt
   ```
   This captures each dependency with a fixed version, which is the canonical way to reproduce a pip-based environment.
2. Update `README.md` with:
   - Clear installation instructions (e.g., `pip install -r requirements.txt` followed by `pip install .`).
   - A description of what the package enables: expected inputs (FASTA proteins), intermediate processing steps (digestion, chromatography, MS simulation), and typical outputs (mz tables, fragment spectra).
   - A short overview of the functions in each module so newcomers immediately know how to run the workflow.
   - A reference to the `ms_experiment_final.ipynb` notebook (placed either in `tutorials/` or the repo root) as an end-to-end example.
3. Use your final experiment notebook as an example on how to use your package. To this end, move or copy the finished notebook into `tutorials/ms_experiment_final.ipynb` (or keep it in the root) and mention its location in the README as the quickest way to try the package.
4. Stage, commit, and push the new `requirements.txt`, README updates, and notebook placement.

Once these steps are complete, your package mirrors the full proteomics pipeline and can be executed end-to-end inside `ms_experiment_final.ipynb`.

🎉 **Congratulations!** You now have a fully documented, tested, and published proteomics package. If your repository is public, anyone can discover it, clone it, or fork it to contribute. If it’s private, only collaborators you invite will see the code, so choose the visibility that fits your goals. Consider mentioning this project in applications or interviews — an GitHub repository showcasing your own functioning bioinformatics package is a strong addition to your portfolio.

## 12. Cross-test for reproducibility
Ensure others can run your package by partnering with a classmate for cross-testing:

1. Exchange GitHub URLs and create a fresh virtual environment dedicated to your partner’s project using conda.
2. Install their package
- directly from GitHub
   ```bash
   pip install git+https://github.com/<partner>/<repo-name>.git
   ```
- from the locally cloned repository
    ``` bash
    git clone https://github.com/<partner>/<repo-name>.git
    cd <repo-name>
    pip install -e .  # -e in case you need to debug
    ```
3. Follow their README to run `ms_experiment_final.ipynb`. You should obtain the same outputs as them (retention-time plots, MS spectra, mz tables). If discrepancies or errors appear, discuss them together and fix documentation or code gaps.
4. Provide feedback on each other’s READMEs — clear installation and usage instructions are what make a package usable by someone new.

This exercise validates that your project is reproducible and helps you spot missing dependencies or unclear directions before sharing it more widely.

## Bonus exercise: LLM-assisted testing and pull requests
Use this optional challenge to practice collaborative workflows and evaluate how LLMs can support (but not replace) your coding and review process:

1. Fork your partner’s repository, then clone your fork locally so all changes stay isolated until you open a pull request.
2. Pick one module that would benefit from stronger tests.
3. Craft an LLM prompt, e.g., “Given the `calculate_mz_collection` function below, write a pytest-style unit test that covers positive charges and invalid inputs.”
4. Review the generated output critically. Note what the LLM did well (coverage ideas, structure) and where it fell short (edge cases, style mismatches, not understanding the biology).
5. Integrate only the portions you trust, editing to match your standards.
6. Create a branch (e.g., `git checkout -b add-llm-test`), add the test, and run `pytest`.
7. Push the branch to the fork and open a pull request describing the LLM-assisted changes. Ask your partner to review, and reciprocate by reviewing theirs.

This reinforces that AI can accelerate ideas, but your judgment, code review, and CI are still essential safeguards.

If you are working on a shared project rather than a fork-and-PR workflow, simply clone the team repository directly and ensure everyone has the necessary push permissions so collaborative branches can be created without forks.
