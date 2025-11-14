# Tutorial 5 – Publish and Collaborate

Day 5 focuses on polishing your project, documenting it for others, and sharing it publicly. You will prepare the repository with a README and license, set up automation, push it to GitHub, and perform collaboration exercises.

---

## 1. Prepare the repository
Before sharing code, make sure newcomers can understand and reuse it.

### 1.1 Write a README
Create a `README.md` in the project root that covers:
- **Project overview:** What does the package do? Mention the proteomics workflow and key functions.
- **Installation:** Show `pip install -e .` plus dependency notes.
- **Usage examples:** Demonstrate core functions (e.g., `read_fasta`, `digest_protein_collection`). Include a link to `[tutorials/ms_simulation_final.ipynb](tutorials/ms_simulation_final.ipynb)` so readers can reproduce the end-to-end pipeline.
- **Testing instructions:** Document the `pytest` command.
- **Results:** Point to the expected TSV outputs or plots.

### 1.2 Choose a license
Select a license that matches your sharing goals (MIT, BSD, Apache 2.0, etc.). Add a `LICENSE` file at the root. GitHub’s license chooser (https://choosealicense.com) can help you decide; once chosen, paste the full text into `LICENSE`.

---

## 2. Set up GitHub Actions for tests
GitHub Actions lets you run automated workflows—like unit tests—every time you push code or open a pull request. This ensures your package remains stable when collaborators contribute.

1. Create `.github/workflows/pytest.yml` in your repo.
2. Configure it to run `pip install -e .` and `pytest` on Ubuntu (and optionally other OS/Python versions).
3. Encourage yourself (and teammates) to rely on LLMs for boilerplate. Example prompt:
   > “Create a GitHub Actions workflow named ‘pytest’ that runs on pushes to `main` and on pull requests. It should set up Python 3.11, install dependencies with `pip install -e .`, and run `pytest`.”
4. Commit the workflow file so GitHub triggers it automatically.

---

## 3. Publish to GitHub
Getting your project onto GitHub makes collaboration and evaluation easier.

1. **Create a new public repository on GitHub** (https://github.com/new). Do not initialize it with a README or license since your local repo already has those files.
2. **Add the remote and push:**
   ```bash
   git remote add origin https://github.com/<username>/<repo>.git
   git branch -M main
   git push -u origin main
   ```
3. **Verify the repository online:** Make sure README, LICENSE, and package files show up on GitHub. Copy the HTTPS URL—you will share it with peers for the collaboration exercise.

---

## 4. Collaboration exercise: cross-test each other’s packages
Pair up with a classmate and test how reproducible your workflows are:

1. Exchange GitHub repository URLs.
2. Clone your partner’s repo, install it in editable mode (`pip install -e .`), and ensure `pytest` passes.
3. Run their `ms_simulation_final.ipynb` (or equivalent) notebook using the shared FASTA file (`data/sample_proteins.fasta`).
4. Compare the generated TSV outputs (`ms1_peptide_mzs.tsv` and `ms2_MATSR_fragment_mzs.tsv`). If your implementations follow the same IO structure and inputs, the results should match.
5. Discuss any discrepancies — are they due to parameter choices, random seeds, or bugs? Submit issues or pull requests if you spot improvements.

This exercise mimics real-world collaboration: reproducibility, clear documentation, and automated tests help peers trust your package.

---

## 5. Optional exercise: LLM-assisted testing and pull requests
Large Language Models (LLMs) can boost productivity, but they follow instructions literally. Always review AI-generated code—treat it like a junior collaborator whose work must be checked.

**Suggested workflow:**

1. Coordinate with your peer and pick a specific test function from their repository (for example, a missing unit test for `calculate_mz_collection`).
2. Check out a commit *before* that test existed (use `git log` / `git checkout <commit>`).
3. Craft an LLM prompt, such as: “Given the `calculate_mz_collection` function below, write a pytest-style unit test that covers positive charges and invalid inputs.”
4. Let the LLM generate the test, then evaluate what it did well (parameter coverage) and where it fell short (missing edge cases, style mismatches).
5. Integrate only the portions you trust, editing as needed to match your standards.
6. Create a new branch (`git checkout -b add-llm-test`), add the test, and run `pytest` locally.
7. Push the branch to your colleague's repository and open a pull request describing the LLM-assisted changes. Ask your partner to review it, and reciprocate by reviewing theirs.

This final exercise reinforces that AI is a powerful helper—but human oversight, code review, and CI tests remain essential.