# Advanced Python Course – Develop a proteomics experiment simulation package

In this five-day hands-on course you turn research-style Python code into a tested,
documented, and installable Python package, and publish it on GitHub. The code simulates
a bottom-up mass-spectrometry proteomics experiment, from protein sequences to simulated
mass spectra.

> [!NOTE]
> **"Advanced"** refers to software development practices (packaging, testing, version
> control, collaboration), not to complex algorithms. The programming itself stays at an
> intermediate level.

## What you will learn
**Software development**
- Structure code into reusable, documented functions
- Write unit tests and run them with `pytest`
- Build an installable Python package (`pyproject.toml`, editable installs)
- Track your work with Git (commit, push, pull, branches)
- Collaborate on GitHub: README documentation, cross-testing, forks, and pull requests
- Run tests automatically with GitHub Actions (continuous integration)
- Create reproducible environments with conda and pip
- Use LLM assistants critically to support your coding

**Scientific Python**
- Data handling and plotting with pandas, NumPy, and Matplotlib
- Text processing with regular expressions
- Using a domain library ([pyteomics](https://pyteomics.readthedocs.io))

**Proteomics basics**
- The bottom-up proteomics workflow: protein digestion, liquid chromatography (LC), and
  mass spectrometry (MS1/MS2)
- Peptide masses, m/z values, and fragment ions

## Prerequisites
**Knowledge**
- Basic Python: data types, loops, conditionals, functions, list and dictionary
  comprehensions
- Some coding experience in any language, ideally at least one small coding project
- Basic command-line navigation (`cd`, `ls`, `mkdir`, `cp`)
- No prior knowledge of proteomics or mass spectrometry is needed. The tutorials
  introduce the concepts.

**Preparation (self-study in the week before the course)**

Everyone starts with a different background, so the week before the course is for
self-organized learning on [DataCamp](https://app.datacamp.com) (the organizers send you
access details) or a platform of your choice. You do not need to do every course. Pick
those that cover what you are not yet familiar with.

*Python basics:* string operations, regular expressions, lists and dictionaries, list and
dictionary comprehensions, slicing, loops, if/else statements, using external libraries,
and simple plots with Matplotlib. These match the contents of the "Standard Python
Course".
- [Introduction to Python for Data Science][dc-intro]
- [Intermediate Python][dc-intermediate-python]
- For looking up specifics: [W3Schools Python](https://www.w3schools.com/python/)

*Developer skills:*
- Writing your own functions: [Introduction to Functions in Python][dc-func]
- Writing and running tests: [Introduction to Testing in Python][dc-testing]
  (chapters 1–3)
- Package development: [Developing Python Packages][dc-packages]
- Version control and collaboration: [Introduction to Git][dc-git] and
  [Introduction to GitHub Concepts][dc-github]

[dc-intro]: https://app.datacamp.com/learn/courses/intro-to-python-for-data-science
[dc-intermediate-python]: https://app.datacamp.com/learn/courses/intermediate-python
[dc-func]: https://app.datacamp.com/learn/courses/introduction-to-functions-in-python
[dc-testing]: https://app.datacamp.com/learn/courses/introduction-to-testing-in-python
[dc-packages]: https://app.datacamp.com/learn/courses/developing-python-packages
[dc-git]: https://app.datacamp.com/learn/courses/introduction-to-git
[dc-github]: https://app.datacamp.com/learn/courses/introduction-to-github-concepts

**Equipment**
- A laptop (Windows, macOS, or Linux) on which you can install software
- The tools from the [setup guide](docs/setup.md), installed **before the course starts**
  (see [Getting started](#getting-started))

## The project
The course simulates a bottom-up proteomics experiment:
- **Input:** a multi-protein FASTA file
  ([sample_proteins.fasta](data/sample_proteins.fasta))
- **Processing:** enzymatic digestion → LC retention-time prediction → MS1/MS2
  simulation (mass, m/z, fragmentation)
- **Output:** TSV files with peptide and fragment m/z values (saved in `results/`),
  diagnostic plots, and your own reusable Python package

Days 1–3 develop the functions in Jupyter notebooks. On days 4–5 you move them into a
package.

## Course overview
| Day | Topic                                     | Material                      |
|-----|-------------------------------------------|-------------------------------|
| 1   | FASTA parsing and protein digestion       | [Tutorial 1][t1]              |
| 2   | Liquid chromatography simulation          | [Tutorial 2][t2]              |
| 3   | MS1/MS2 spectra simulation                | [Tutorial 3][t3]              |
| 4   | Package your functions, with tests and CI | [Tutorial 4][t4]              |
| 5   | Publish, cross-test, and pull requests    | [Tutorial 4][t4], [Bonus][t5] |

The [final notebook][final] runs the complete experiment with your package. A reference
solution of the package is available at [UKHD-NP/proteosim][proteosim]. Try it yourself
first.

[t1]: tutorials/1_protein_digestion.ipynb
[t2]: tutorials/2_liquid_chromatography.ipynb
[t3]: tutorials/3_mass_spectra_simulation.ipynb
[t4]: tutorials/4_build_and_publish_your_own_package.md
[t5]: tutorials/5_bonus_exercises.md
[final]: tutorials/ms_simulation_final.ipynb
[proteosim]: https://github.com/UKHD-NP/proteosim

## Getting started
Before the course, follow the setup guide: **[docs/setup.md](docs/setup.md)**. It covers
the GitHub account and access token, Git, VS Code, Conda (via Miniforge), the course
environment, an LLM assistant, and a Google Colab fallback.

## Working on the tutorials
Do not edit the tutorial notebooks directly. Work on your own copy instead.

**Why:** the instructors may update the tutorials during the course. If you edit the
original notebooks, `git pull` fails with conflicts and you have to sort out your changes
and ours by hand. If you only edit copies, `git pull` always works.

At the start of each tutorial:
1. Get the latest version of the course material (in the terminal, inside
   `advanced-python_course`):
   ```bash
   git pull
   ```
2. Copy the notebook of the day into the **same** `tutorials/` folder and add `_edit` to
   the name. It must stay in `tutorials/`, because the notebooks read from `../data` and
   write to `../results`.
3. Open and work only in the `_edit` copy. Leave the original unchanged.

## Folder structure
```
.
├── data/          # Input FASTA files
├── tutorials/     # Day-by-day notebooks (days 1–3) and instructions (days 4–5)
├── templates/     # pyproject.toml template for your package
├── results/       # Outputs written by the tutorials
├── docs/          # Setup guide and course slides
└── README.md
```

## For the course organizers
- Provide clear instructions on how to obtain access to Datacamp and its courses with two
  weeks in advance
- Ensure there enough power outlets in the room for the practical part.

## Improvements for next iteration of the course

### Student feedback
- [ ] For some more students advanced students the first tutorials were too easy, too
  much was given. Solution? Hide proposed code under "hints" foldable sections. This way
  advanced students have a greater challenge while less advanced can still profit from
  templates.

### Content improvement
- [ ] For exercise 5.12 use the E.coli fasta file and ask the students to compare
  different proteases as well as to plot the distribution of nr. of peptides per protein
  (fasta file already included in repo).
