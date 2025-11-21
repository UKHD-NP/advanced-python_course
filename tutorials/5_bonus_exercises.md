# Bonus exercises

## 1. LLM-assisted testing with forks and pull requests
Use this optional challenge to practice real-world collaboration and evaluate how LLMs can support (but not replace) your coding and review process. Two collaborators with direct write access can work in the same repository without forking, but that requires tight coordination so no one overwrites another person’s work. To safely separate changes this time, you will fork the repository and contribute back through a pull request (PR).

1. Fork your partner’s repository on GitHub. The fork is your personal copy where you can experiment freely without affecting their default branch.
2. Clone your fork locally (`git clone <your-fork-url>`) and set the original repository as the `upstream` remote so you can pull updates if needed.
3. Pick one module that would benefit from stronger tests.
4. Craft an LLM prompt, e.g., “Given the `calculate_mz_collection` function below, write a pytest-style unit test that covers positive charges and invalid inputs.”
5. Review the generated output critically. Note what the LLM did well (coverage ideas, structure) and where it fell short (edge cases, style mismatches, not understanding the biology).
6. Create a feature branch in your fork (e.g., `git checkout -b add-llm-test`), integrate only the code you trust, and run `pytest`.
7. Push the branch to your fork (`git push origin add-llm-test`).
8. On GitHub, open a pull request from your forked branch into your partner’s default branch. A good PR summarizes the intent, explains how you validated the changes, and calls out anything reviewers should double-check. See the [GitHub pull request guide](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests) for more details.
9. Ask your partner to review, and reciprocate by reviewing theirs. Focus on the usual PR quality signals: clear description, small scope, passing tests, and thoughtful code comments when needed.

This workflow reinforces that AI can accelerate ideas, but your judgment, code review, and CI remain essential safeguards when collaborating through forks and pull requests.
