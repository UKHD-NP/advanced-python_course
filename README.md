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
- **Day 4:** Build a reusable Python package from the functions ([4_build_your_own_package.md](4_build_your_own_package.md))
- **Day 5:** Publish the package, set up CI, and collaborate ([tutorials/5_publish_your_package.md](tutorials/5_publish_your_package.md))

A final notebook ([tutorials/ms_simulation_final.ipynb](tutorials/ms_simulation_final.ipynb)) ties the package together for an end-to-end experiment.

## Getting started
1. Clone this repository.
2. Install dependencies from `requirements.txt` (e.g., via `pip install -r requirements.txt`) and follow each tutorial in order.

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
## Recommendations
If you work in Google Colab, mount your Drive and switch into the repository folder so notebooks can read/write data:

```python
# Mount the Google Drive for Colab users
from google.colab import drive
drive.mount('/content/drive')

import os

notebook_filename = '1_protein_digestion.ipynb'
notebook_path = None

for root, dirs, files in os.walk('/content/drive/MyDrive'):
    if notebook_filename in files:
        notebook_path = root
        break

if notebook_path:
    os.chdir(notebook_path)
    print("Directory changed to:", notebook_path)
else:
    print(f"Notebook file '{notebook_filename}' not found in Google Drive.")
```
