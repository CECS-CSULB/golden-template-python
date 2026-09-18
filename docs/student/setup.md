# Student Setup Guide

This project contains a Python package under `src/` and a `pytest` suite under
`tests/`. The sample assignment asks you to implement `mean`, `median`, and
`mode` in `src/stats.py`.

You need:

- Python 3.12, matching continuous integration.
- Git, if you cloned the project or will push it to GitHub.
- An internet connection the first time `pip` installs packages from
  `requirements.txt`.

Run all project commands from the repository root—the directory containing
`requirements.txt`, `src/`, and `tests/`.

## Windows setup

### 1. Install Python

Install Python 3.12 from [python.org](https://www.python.org/downloads/) or with
Windows Package Manager:

```powershell
winget install --id Python.Python.3.12 -e
```

Close and reopen PowerShell, then verify the launcher:

```powershell
py -3.12 --version
```

### 2. Install dependencies

From the repository root:

```powershell
py -3.12 -m pip install --upgrade pip
py -3.12 -m pip install -r requirements.txt
```

## macOS setup

### 1. Install Python

Install Python 3.12 from [python.org](https://www.python.org/downloads/) or with
[Homebrew](https://brew.sh/):

```bash
brew install python@3.12
```

Verify the interpreter:

```bash
python3.12 --version
```

### 2. Install dependencies

From the repository root:

```bash
python3.12 -m pip install --upgrade pip
python3.12 -m pip install -r requirements.txt
```

## Linux or WSL setup

Install Python 3, pip, and Git using your distribution's package manager. On
Ubuntu or WSL Ubuntu:

```bash
sudo apt update
sudo apt install -y python3 python3-pip git
```

Then install the project dependencies from the repository root:

```bash
python3 -m pip install --upgrade pip
python3 -m pip install -r requirements.txt
```

For better WSL filesystem performance, keep the repository in the Linux
filesystem, such as `~/projects/cecs-golden-template-python`, rather than under
`/mnt/c`.

## Run the tests

On macOS, Linux, or WSL:

```bash
python3 -m pytest -q
```

On Windows PowerShell:

```powershell
py -3.12 -m pytest -q
```

The untouched starter is intentionally incomplete, so its tests fail with
`NotImplementedError`. That confirms the tests are reaching the starter code.
As you implement each function, rerun the suite and use the named failures as
feedback.

To check that pytest can discover the suite without executing the test bodies:

```bash
python3 -m pytest --collect-only -q
```

The sample project should collect twelve tests.

## Try the module interactively

This sample is a library assignment rather than a command-line application.
After implementing the functions, you can call one from the repository root:

```bash
python3 -c "from src.stats import mean; print(mean([1, 2, 3, 4]))"
```

The expected output is `2.5`. The automated tests are the authoritative check
for all required behavior.

## Common problems

### `python`, `python3`, or `py` is not found

Close and reopen the terminal after installing Python. On Windows, use the
`py -3.12` launcher. On macOS or Linux, try `python3` or `python3.12`. Confirm
the selected version:

```bash
python3 --version
```

### `No module named pytest`

Install the requirements again with the same interpreter used to run pytest:

```bash
python3 -m pip install -r requirements.txt
python3 -m pytest -q
```

On Windows, use `py -3.12` in place of `python3`.

### pip reports a permission or managed-environment error

Do not use `sudo pip` or disable your operating system's package protections.
Confirm that you installed Python using the method approved for your course,
then ask your instructor or lab administrator which Python installation to
use.

### `No module named src`

Change to the repository root before running pytest. Do not run
`python tests/test_stats.py` directly.

```bash
cd /path/to/cecs-golden-template-python
python3 -m pytest -q
```

### Tests fail with `NotImplementedError`

That is expected until you replace the starter bodies in `src/stats.py`.
Implement one function at a time, keep the required names and signatures, and
rerun the tests.
