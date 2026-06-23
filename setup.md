# L01 Setup — Environment Guide

This guide gets you from zero to running L01 on your machine in about 15 minutes. The same environment works for every lesson in the DSAI M3 series.

**Supported environments:**
- **macOS** (Apple Silicon — M1 or later)
- **Windows 10/11 with WSL2** (Ubuntu 22.04 recommended)
- **Google Colab** (handy fallback if local install gives trouble)

**Supported IDE / runtime:**
- **VS Code + Jupyter extension** (recommended)
- **Google Colab** (browser-based fallback)

You do **not** need Jupyter Notebook or JupyterLab installed separately — VS Code handles everything.

---

## TL;DR — fastest path

```bash
# 1. Clone the repo
git clone https://github.com/su-ntu-ctp/6m-data-3.1-Introduction-to-Machine-Learning.git
cd 6m-data-3.1-Introduction-to-Machine-Learning

# 2. Create the conda environment
conda env create -f environment.yml
conda activate dsai-m3

# 3. Install the L01 extras (Hugging Face transformers + torch)
pip install transformers torch

# 4. Launch VS Code in the repo root
code .
```

Then in VS Code:
1. Open `notebooks/02_what_is_ml.ipynb`
2. Top-right → **Select Kernel** → `dsai-m3` (Python 3.11)
3. **Run All**

If a notebook hangs or errors, scroll down to **Troubleshooting**.

---

## 1. Install Python via Miniconda

We use conda to manage a self-contained Python environment for the course. This avoids polluting your system Python.

### macOS (Apple Silicon)

```bash
curl -L https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-arm64.sh -o miniconda.sh
bash miniconda.sh -b -p $HOME/miniconda3
$HOME/miniconda3/bin/conda init "$(basename $SHELL)"

# Restart your terminal, then verify
conda --version
```

### Windows WSL (Ubuntu)

Open Ubuntu in WSL, then:

```bash
curl -L https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o miniconda.sh
bash miniconda.sh -b -p $HOME/miniconda3
$HOME/miniconda3/bin/conda init bash

# Restart your terminal, then verify
conda --version
```

> **Windows users — do NOT install Miniconda on Windows directly.** Use WSL. Notebooks that use PyTorch are much more reliable on Linux (WSL is Linux) than native Windows.

---

## 2. Clone the repo

### macOS

```bash
mkdir -p ~/repos
cd ~/repos
git clone https://github.com/su-ntu-ctp/6m-data-3.1-Introduction-to-Machine-Learning.git
cd 6m-data-3.1-Introduction-to-Machine-Learning
```

### Windows WSL

Clone **inside WSL**, not in the Windows file system. Notebooks run *much* faster on the WSL filesystem (`~/repos/...`) than on `/mnt/c/...`.

```bash
mkdir -p ~/repos
cd ~/repos
git clone https://github.com/su-ntu-ctp/6m-data-3.1-Introduction-to-Machine-Learning.git
cd 6m-data-3.1-Introduction-to-Machine-Learning
```

---

## 3. Create the conda environment

From the cloned repo root:

```bash
conda env create -f environment.yml
conda activate dsai-m3
```

This creates an environment named `dsai-m3` with Python 3.11 and the L01 baseline packages.

### Install L01-specific extras

L01 uses pretrained sentiment / NLP models via Hugging Face's `transformers` library:

```bash
pip install transformers torch
```

Versions known to work:
- `torch >= 2.2`
- `transformers >= 4.40`

---

## 4. Install VS Code + Jupyter extension

### macOS

Download from https://code.visualstudio.com/Download. Drag to Applications.

### Windows WSL

Install VS Code **on Windows** (not in WSL). VS Code itself runs on Windows; it connects to WSL through the Remote-WSL extension. Download from https://code.visualstudio.com/Download.

### Required extensions (both platforms)

In VS Code, **Cmd/Ctrl+Shift+X** opens the Extensions sidebar. Install:

1. **Python** (Microsoft) — required
2. **Jupyter** (Microsoft) — required
3. **WSL** (Microsoft) — **only for Windows WSL users**; lets you open the WSL filesystem from VS Code

---

## 5. Open the repo in VS Code

```bash
cd ~/repos/6m-data-3.1-Introduction-to-Machine-Learning
code .
```

On WSL this launches VS Code with WSL on the backend. You'll see a green `WSL: Ubuntu` indicator in the bottom-left.

---

## 6. Verify your setup

Open `notebooks/02_what_is_ml.ipynb`.

1. **Top-right of the notebook → "Select Kernel"** → pick `dsai-m3` (Python 3.11)
2. Run the **first code cell** (`import pandas as pd...`)
3. You should see `✅ Libraries loaded — you're ready to go!`

The first time you run cell 9 (the pipeline load), it downloads `distilbert-base-uncased-finetuned-sst-2-english` (~268 MB) from Hugging Face into `~/.cache/huggingface/`. This takes 30 sec to 2 min depending on your connection. After that it's cached locally and the load is instant.

The whole notebook should complete in under 3 minutes (including the first-run download). No dataset to download separately — L01 uses 5–25 hand-crafted product reviews defined directly in the notebooks.

---

## When to use Google Colab instead

If local install is giving you trouble, you can run any notebook in **Google Colab** (free tier). Upload the `.ipynb` file or open it via **File → Open notebook → GitHub** and paste this repo's URL.

**Colab caveats:**
- Free-tier sessions expire after ~12 hours; save your work
- File system is ephemeral — anything you write is lost when the session ends

For L01 specifically, CPU is fine; you don't need a GPU.

---

## Troubleshooting

### "The notebook hangs forever when I run the sentiment model" (NB02)

This is the OpenMP scheduler issue on macOS — PyTorch threads can lock up the CPU. Cap the thread count in your shell before launching VS Code:

```bash
export OMP_NUM_THREADS=1
code .
```

Or create a `.env` file at the repo root with:

```
OMP_NUM_THREADS=1
```

**Verify the env var loaded** — in any code cell:

```python
import os
print(os.environ.get("OMP_NUM_THREADS"))   # should print "1"
```

If VS Code's kernel itself is stuck and **Restart Kernel** hangs:

```bash
# In a fresh terminal
pkill -9 -f ipykernel
pkill -9 -f vscode-jupyter
```

Then reload VS Code (Cmd+Q + relaunch).

### "I get a `ModuleNotFoundError` for torch / transformers"

You skipped the L01 extras step. Run:

```bash
conda activate dsai-m3
pip install transformers torch
```

### "Kernel `dsai-m3` doesn't appear in the kernel picker"

VS Code's Python extension caches kernels. Reload VS Code:
**Cmd/Ctrl+Shift+P → "Developer: Reload Window"**

If still missing:

```bash
conda activate dsai-m3
python -m ipykernel install --user --name dsai-m3 --display-name "Python (dsai-m3)"
```

Then reload VS Code again.

### "WSL is slow"

You're probably running notebooks from `/mnt/c/...` (the Windows filesystem). Move them to `~/repos/...` inside WSL — notebook execution gets 5–10× faster.

### Something else broke

Open an issue: https://github.com/6m-data-3.1-Introduction-to-Machine-Learning/issues. Include:
- macOS or WSL? (and version)
- Output of `conda --version`, `python --version`, `pip show torch transformers`
- The full error traceback
- Which notebook + which cell

---

## Quick reference

| Task | Command |
|---|---|
| Activate the env | `conda activate dsai-m3` |
| Update deps | `pip install -U transformers torch` |
| Launch VS Code in repo | `code .` (from the repo root) |
| Force-kill stuck kernel | `pkill -9 -f ipykernel` |
| Reload VS Code | `Cmd/Ctrl+Shift+P → "Developer: Reload Window"` |
