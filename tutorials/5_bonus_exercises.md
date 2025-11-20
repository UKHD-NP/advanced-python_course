# Bonus exercises

## 1. LLM-assisted testing and pull requests
Use this optional challenge to practice collaborative workflows and evaluate how LLMs can support (but not replace) your coding and review process:

1. Fork or clone your partner’s repository. If you lack push access or want to protect their default branch, fork the repo first, then clone your fork locally so all changes stay isolated until you open a pull request.
2. Pick one module that would benefit from stronger tests.
3. Craft an LLM prompt, e.g., “Given the `calculate_mz_collection` function below, write a pytest-style unit test that covers positive charges and invalid inputs.”
4. Review the generated output critically. Note what the LLM did well (coverage ideas, structure) and where it fell short (edge cases, style mismatches, not understanding the biology).
5. Integrate only the portions you trust, editing to match your standards.
6. Create a branch (e.g., `git checkout -b add-llm-test`), add the test, and run `pytest`.
7. Push the branch to the fork and open a pull request describing the LLM-assisted changes. Ask your partner to review, and reciprocate by reviewing theirs.

This reinforces that AI can accelerate ideas, but your judgment, code review, and CI are still essential safeguards.
