# Advanced Python Course – Proteomics Pipeline

This repository hosts a five-day intensive course that teaches advanced Python package development practices through a simulated mass-spectrometry proteomics workflow.

## Simulated proteomics pipeline
The course emulates a bottom-up proteomics experiment:
- **Input:** Multi-protein FASTA file: [sample_proteins.fasta](data/sample_proteins.fasta).
- **Processing:** Enzymatic digestion → LC retention-time prediction → MS1/MS2 simulation (mass, m/z, fragmentation).
- **Output:** TSV files summarizing peptide/fragment m/z values (stored under `results/`), diagnostic plots, and a reusable Python package.

## Course overview
- **Day 1:** FASTA parsing and protein digestion fundamentals ([tutorials/1_protein_digestion.ipynb](tutorials/1_protein_digestion.ipynb))
- **Day 2:** Liquid chromatography simulation ([tutorials/2_liquid_chromatography.ipynb](tutorials/2_liquid_chromatography.ipynb))
- **Day 3:** MS1/MS2 spectra simulation ([tutorials/3_mass_spectra_simulation.ipynb](tutorials/3_mass_spectra_simulation.ipynb))
- **Day 4:** Build a reusable Python package from the functions ([tutorials/4_build_your_own_package.md](tutorials/4_build_your_own_package.md))
- **Day 5:** Publish the package, set up CI, and collaborate ([tutorials/5_publish_your_package.md](tutorials/5_publish_your_package.md))

A final notebook ([tutorials/ms_simulation_final.ipynb](tutorials/ms_simulation_final.ipynb)) ties the package together for an end-to-end experiment.

## Getting started
Before the course, follow the setup guide: **[docs/setup.md](docs/setup.md)**. It covers the GitHub account and access token, Git, VS Code, Conda (via Miniforge), the course environment, and a Google Colab fallback.

## Folder structure
```
.
├── data/                      # Input FASTA files
├── tutorials/                 # Day-by-day Jupyter notebooks
├── templates/                 # pyproject.toml and packaging scaffolds
├── results/                   # Output TSVs saved by tutorials
├── docs/                      # Reference materials
└── README.md
```
## Improvements for next iteration of the course
### Student feedback
- [ ] Advertise the course better to the students: "advanced" python in the
  sene that they learned package development skills, not that they learn how to
  write more complex algorithms and code. Also communicate the coding skill
  requirements well. Probably via HeiCo.
- [ ] Provide clear instructions on how to obtain access to Datacamp WELL in advance
- [ ] Testing course on Datacamp may have been overkill since we only used simple testing functions
- [ ] Conda/VScode/Gcollab/environment setup session prior to practical week to
  avoid overhead to actual tutorials. Maybe even with a script?
- [ ] Problem: cloning repo and working direclty inside hinders pulling of changes to the tutorials. Solution? Work on tutorials in a separate directory
- [ ] Great clarity, structure and objective setting, but for some more
  advanced students the first tutorials were too easy, too much was given.
  Solution? Hide proposed code under "hints" foldable sections. This way
  advanced students have a greater challenge while less advanced can still
  profit from templates.
- [ ] For bigger groups, ensure enough power outlets in the room.
### Content improvement
- [ ] For exercise 5.12 use the E.coli fasta file and ask the students to compare different proteases as well as to plot the distribution of nr. of peptides per protein (fasta file already included in repo).
