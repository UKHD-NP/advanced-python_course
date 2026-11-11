# Course Setup

During the course you will write code, track it with version control, share it on GitHub, and turn it into an installable Python package. Each of these steps needs a tool on your own computer. Please set everything up **before the practical part of the course starts**, so the course days can be spent on the tutorials and not on installation problems. The setup takes about 30–60 minutes.

Every step ends with a **✅ Check**. If you get stuck, note the error message and send us a message or bring it to the debugging session.

> 💡 **Local setup not working at all?** You can still follow Tutorials 1–3 in the browser with Google Colab. See [5. Google Colab fallback](#5-google-colab-fallback).

## Contents
0. [Overview](#overview)
1. [GitHub account and access token](#1-github-account-and-access-token)
2. [Software](#2-software)
   1. [Git](#21-git)
   2. [VS Code](#22-vs-code)
   3. [VS Code extensions](#23-vs-code-extensions)
   4. [Conda (via Miniforge)](#24-conda-via-miniforge)
3. [Course environment](#3-course-environment)
4. [LLM assistant](#4-llm-assistant)
5. [Google Colab fallback](#5-google-colab-fallback)

## Overview

| Item | Why you need it |
|---|---|
| GitHub account | Hosts your code online so you can share it and work with others |
| GitHub access token | Your password for `git push` from the terminal |
| Git | Version control: tracks every change to your code |
| VS Code | Coding environment: edit code and run notebooks |
| Python + Jupyter extensions | Let VS Code run Python code and Jupyter notebooks |
| Conda (Miniforge) | Creates isolated Python environments for each project |
| Course environment | The Python version and packages used in the tutorials |
| LLM assistant | Helps with debugging and drafting code |

---

## 1. GitHub account and access token

### 1.1 Create a GitHub account
**Why:** collaboration. You will publish your package on GitHub and work on a partner's repository.

Sign up for free at <https://github.com/signup>. If you already have an account, you can use it.

> 🎓 Optional: as a student you can apply for the free [GitHub Student Developer Pack](https://education.github.com/pack). It includes GitHub Copilot (see [4. LLM assistant](#4-llm-assistant)).

✅ **Check:** you can log in at <https://github.com> and you can see your profile picture in the top-right corner.

### 1.2 Create a Personal Access Token (classic)
**Why:** authentication. GitHub does not accept your account password for `git push` from the terminal. The token is used in its place.

1. On <https://github.com>, click your **profile picture** (top right) → **Settings**.
2. Scroll down the left sidebar and click **Developer settings** (the last entry).
3. Click **Personal access tokens** → **Tokens (classic)**.
4. Click **Generate new token** → **Generate new token (classic)**. Confirm your password if GitHub asks for it.
5. Fill in the form:
   - **Note:** `advanced-python-course`
   - **Expiration:** choose a date after the end of the course (e.g. 90 days)
   - **Select scopes:** tick **`repo`** and **`workflow`**. You need `workflow` to push GitHub Actions files in Tutorial 4.
6. Scroll down and click **Generate token**.
7. **Copy the token now** (it starts with `ghp_`) and save it in a password manager or a safe note. GitHub shows it **only once**. If you lose it, delete it and create a new one.

When `git push` asks you for a password, paste this token. You will not see the characters while you paste, which is normal.

> ⚠️ Treat the token like a password. Never put it in code, notebooks, or commits.

✅ **Check:** under **Settings → Developer settings → Personal access tokens → Tokens (classic)**, your token `advanced-python-course` is listed with the scopes `repo, workflow`, and you have the token saved.

---

## 2. Software

In this guide, **terminal** means:
- **macOS:** the *Terminal* app
- **Linux:** your usual terminal
- **Windows:** *Git Bash*, which is installed together with Git in [2.1](#21-git). Use Git Bash for all commands in this course.

### 2.1 Git
**Why:** version control. Git tracks every change to your code and pushes it to GitHub.

**macOS**
```bash
xcode-select --install
```
Alternatively, if you use [Homebrew](https://brew.sh): `brew install git`.

**Linux**
```bash
sudo apt install git     # Debian / Ubuntu
sudo dnf install git     # Fedora
```

**Windows**
1. Download the installer from <https://git-scm.com/downloads/win>.
2. Run it and keep the default options, with two changes:
   - *Choosing the default editor used by Git:* select **Visual Studio Code** (or keep the default if you have not installed VS Code yet).
   - *Adjusting the name of the initial branch:* select **Override** and keep `main`.
3. After the installation, open **Git Bash** from the Start menu.

✅ **Check** (in the terminal):
```bash
git --version
```
This prints a version, e.g. `git version X.XX.X`.

#### Configure your identity
**Why:** every commit records who made it. This matters when you work on a partner's repository in the collaboration part of the course. Git refuses to commit until this is set.

Run this on all operating systems (Windows: in Git Bash). Use the same email address as your GitHub account:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
```

✅ **Check:**
```bash
git config --global --list
```
The output shows your `user.name`, `user.email`, and `init.defaultbranch=main`.

### 2.2 VS Code
**Why:** coding environment. You will edit code, run notebooks, and use the terminal in one place.

Download and install it for your operating system from <https://code.visualstudio.com/download>.

✅ **Check:** VS Code starts. Open the built-in terminal with **View → Terminal**.
> Windows: in the terminal panel, click the **˅** next to **+** and select **Git Bash**. To make it the default, use **Terminal: Select Default Profile** from the Command Palette (`Ctrl+Shift+P`).

### 2.3 VS Code extensions
**Why:** they let VS Code run Python code and Jupyter notebooks.

Open the Extensions view (left sidebar, or `Ctrl+Shift+X` / `Cmd+Shift+X` on macOS). Search for these extensions and click **Install**:

| Search for | Publisher |
|---|---|
| `Python` | Microsoft |
| `Jupyter` | Microsoft |

✅ **Check:** both extensions appear under **Installed** in the Extensions view. Open the Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`) and type `Create: New Jupyter Notebook`. The command is listed.

### 2.4 Conda (via Miniforge)
**Why:** environment management. Conda installs Python and packages into separate environments, so different projects do not break each other.

> Already have Anaconda or Miniconda? You can skip this step.

Miniforge is a minimal installer for `conda` that installs packages from the free community channel *conda-forge*.

Install Miniforge by following the **Install** section for your operating system on the official page: <https://github.com/conda-forge/miniforge>

- **macOS / Linux:** when the installer asks whether to initialize your shell (`conda init`), answer **yes**. Then close and reopen the terminal.
- **Windows:** after the installation, open **Miniforge Prompt** from the Start menu and run the following command to make `conda` available in Git Bash:
  ```
  conda init bash
  ```
  Then close everything and open a new **Git Bash**.

✅ **Check** (in a new terminal):
```bash
conda --version
```
This prints a version number. Your prompt now starts with `(base)`.

---

## 3. Course environment
**Why:** it contains the exact Python version and packages the tutorials use, separate from all other Python installations on your computer.

Clone the course repository and create the environment:
```bash
git clone https://github.com/UKHD-NP/advanced-python_course.git
cd advanced-python_course

conda create -n advanced-python_course python=3.10 -y
conda activate advanced-python_course
pip install -r requirements.txt ipykernel pytest
```
- `ipykernel` lets the environment run Jupyter notebooks.
- `pytest` runs the unit tests in Tutorial 4.

✅ **Check:**
```bash
python --version
python -c "import numpy, pandas, matplotlib, pyteomics; print('All packages OK')"
```
The first command prints `Python 3.10.x`. The second prints `All packages OK`.

### Register the environment for VS Code / Jupyter
**Why:** VS Code then lists the environment as a notebook kernel.

With the environment still activated, run:
```bash
python -m ipykernel install --user --name advanced-python_course --display-name "Python (advanced-python_course)"
```

✅ **Check:**
1. In VS Code, **File → Open Folder…** and select `advanced-python_course`. Open `tutorials/1_protein_digestion.ipynb`.
2. Click **Select Kernel** (top right) → **Jupyter Kernel…** (or **Python Environments…**) → **Python (advanced-python_course)**.
3. Create a new code cell, run `import pyteomics; print("Kernel OK")`, and make sure it prints `Kernel OK`. Delete the cell afterwards.

> If the kernel does not show up, restart VS Code.

---

## 4. LLM assistant
**Why:** coding help. Parts of the course (e.g. writing the GitHub Actions workflow and the bonus exercises) suggest using an LLM to draft code, explain errors, or write tests.

Any of these works. Create an account for at least one:
- [ChatGPT](https://chatgpt.com)
- [Claude](https://claude.ai)
- [Gemini](https://gemini.google.com)
- [GitHub Copilot](https://github.com/features/copilot), which works directly inside VS Code. It is free for verified students through the [GitHub Student Developer Pack](https://education.github.com/pack).

> Never paste tokens, passwords, or unpublished/sensitive data into an LLM. Always read and test generated code before using it.

✅ **Check:** you can log in and get an answer to a simple question, e.g. *"What does `git status` do?"*

---

## 5. Google Colab fallback
**Why:** a browser-only fallback if the local setup does not work at all. You only need a Google account.

> ⚠️ Colab works for the notebooks (Tutorials 1–3). Building and publishing your own package (Tutorial 4 onwards) needs the local setup. Fix it together with the instructors before Day 4.

### 5.1 Get the repository into Google Drive
1. Go to <https://colab.research.google.com> and create a **New notebook**.
2. Run this in a cell (allow access to your Google Drive when asked):
   ```python
   from google.colab import drive
   drive.mount('/content/drive')

   !git clone https://github.com/UKHD-NP/advanced-python_course.git /content/drive/MyDrive/advanced-python_course
   ```

✅ **Check:** in Google Drive, the folder `My Drive/advanced-python_course` exists and contains `tutorials/` and `data/`.

### 5.2 Open a tutorial and switch into its folder
Open a tutorial notebook from Google Drive (right-click → **Open with → Google Colaboratory**). At the top of the notebook, add a cell that installs the missing package, mounts your Drive, and switches into the repository folder so the notebook can read and write data. Pick the snippet that fits your situation.

**1. You already know where the repo lives**
```python
!pip install -q pyteomics

from google.colab import drive
drive.mount('/content/drive')

import os

repo_path = '/content/drive/MyDrive/advanced-python_course/tutorials'
os.chdir(repo_path)
print('Directory changed to:', os.getcwd())
```

**2. You only know the notebook name**
```python
!pip install -q pyteomics

from google.colab import drive
drive.mount('/content/drive')

import os

target_notebook = '1_protein_digestion.ipynb'
notebook_dir = None

for root, _, files in os.walk('/content/drive/MyDrive'):
    if target_notebook in files:
        notebook_dir = os.path.dirname(os.path.join(root, target_notebook))
        break

if notebook_dir:
    os.chdir(notebook_dir)
    print('Directory changed to:', notebook_dir)
else:
    print(f"Notebook '{target_notebook}' not found in Google Drive.")
```

✅ **Check:** the cell prints `Directory changed to: .../tutorials`, and `import pyteomics` runs without an error.
