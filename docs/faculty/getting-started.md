# Getting Started with the Python Code Template

This guide explains how to turn the sample statistics exercise into a different
Python assignment while keeping imports, dependencies, tests, and CI aligned.

The central rule is simple: whenever you rename a module, function, or test,
update every place that imports or invokes it. Python does not need a separate
build manifest for source files, but the test suite, CI workflow, and Classroom
50 grading configuration still form one contract.

## Start by understanding the current layout

```text
src/
├── __init__.py          # Marks src as a package
└── stats.py             # Starter functions students implement
tests/
└── test_stats.py        # Public pytest cases
requirements.txt         # Python dependencies, including pytest
.github/workflows/ci.yml # Collection check in the template; full tests in copies
VERIFICATION-LOG.md      # Student AI-assistance record
```

The sample module exports `mean`, `median`, and `mode`. Each stub raises
`NotImplementedError`, and the public suite contains twelve cases. CI installs
`requirements.txt`, imports the project, and either collects or runs those
tests depending on whether GitHub identifies the repository as a template.

Keep `src/__init__.py` unless you intentionally choose a different package
layout. Commands in this repository run from its root, which lets tests import
modules such as `src.stats` without installing the project as a package.

## Read the important files as one project map

[`src/stats.py`](../../src/stats.py) defines the assignment's public contract.
Its docstrings describe expected behavior and edge cases. An unfinished
function raises explicitly:

```python
def mean(values):
    """Return the arithmetic mean of a non-empty sequence."""
    raise NotImplementedError("implement mean()")
```

Prefer `raise NotImplementedError` to `pass`. A bare `pass` returns `None`, so
an untouched stub becomes indistinguishable from a student's incorrect
implementation in test output.

[`tests/test_stats.py`](../../tests/test_stats.py) imports that public contract:

```python
import pytest

from src.stats import mean


def test_empty_raises():
    with pytest.raises(ValueError):
        mean([])
```

[`requirements.txt`](../../requirements.txt) lists packages that must be
installed before tests run. The current file contains `pytest>=8.0`.

Finally, [`.github/workflows/ci.yml`](../../.github/workflows/ci.yml) records the
supported Python version, dependency-install command, test command, and
expected number of collected cases. Treat those values as part of the project
map too.

## Replace the assignment in a controlled order

### 1. Define the assignment contract

Before editing files, write down:

- The modules students may edit.
- Required functions, classes, signatures, and return values.
- Required exceptions or other behavior for invalid input.
- Whether students may add dependencies or change public interfaces.
- Which tests are public and whether hidden tests exist.

Put the student-facing version in
[`STUDENT_README.md`](../../STUDENT_README.md). A tested edge case must also be
a documented edge case.

### 2. Replace the starter module

Replace `src/stats.py` with the module or modules for the new exercise. For
example:

```text
src/
├── __init__.py
├── queue.py
└── node.py
```

Use small, importable modules when the subject permits it. Avoid doing input,
network, or filesystem work at import time: a side effect that fails during
collection prevents every test from running.

For an intentionally incomplete method, keep a precise docstring and raise:

```python
class Queue:
    def enqueue(self, value):
        """Add value to the back of the queue."""
        raise NotImplementedError("implement Queue.enqueue()")
```

If the assignment includes a command-line program, put execution behind the
standard guard so importing the module remains safe:

```python
def main():
    ...


if __name__ == "__main__":
    main()
```

Students can then run it with `python3 -m src.your_module`, while tests can
import it without launching the program.

### 3. Replace the tests

Replace `tests/test_stats.py` with files named `test_*.py` so pytest discovers
them automatically. Import from the same public paths students are told to
implement:

```python
from src.queue import Queue


def test_fifo_order():
    queue = Queue()
    queue.enqueue("first")
    queue.enqueue("second")
    assert queue.dequeue() == "first"
```

Prefer one behavior per test. Classroom 50 can divide a pytest test entry's
points across the cases it reports, so test count influences weighting. Keep
tests deterministic: avoid live network calls, the real clock, uncontrolled
randomness, and writes outside pytest's temporary-directory fixtures.

If the number of cases changes, update `EXPECTED_CASES` in
`.github/workflows/ci.yml`. That value protects the template from accidentally
losing tests while the starter implementations are still incomplete.

### 4. Update dependencies

Add only runtime and test dependencies the assignment actually imports:

```text
pytest>=8.0
requests>=2.32
```

Then verify installation in a fresh virtual environment. If packages have
platform-specific requirements or need exact versions for reproducible
grading, document and pin them deliberately.

Do not put standard-library modules such as `collections`, `statistics`, or
`unittest` in `requirements.txt`.

### 5. Update every command and import

Search for the old sample names before publishing:

```bash
rg "stats|mean|median|mode|test_stats"
```

Update at least:

- Imports in `tests/`.
- The import smoke test and test path in Classroom 50.
- `EXPECTED_CASES` and any commands in `.github/workflows/ci.yml`.
- Student instructions and examples.
- Comments or documentation that describe the old exercise.

The default CI command `python3 -m pytest -q` can usually remain unchanged when
tests keep pytest's discovery names.

## Install and test the adapted project

Use an isolated environment so the verification does not depend on packages
already installed globally.

On macOS, Linux, or WSL:

```bash
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install --upgrade pip
python3 -m pip install -r requirements.txt
python3 -m pytest --collect-only -q
python3 -m pytest -q
```

On Windows PowerShell:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
py -m pip install --upgrade pip
py -m pip install -r requirements.txt
py -m pytest --collect-only -q
py -m pytest -q
```

The untouched template is expected to collect twelve tests and fail them when
run, because the starter functions are deliberately unimplemented. Before
publishing, verify both sides of the grading signal:

1. A known-correct solution passes the full suite.
2. A deliberately wrong solution fails with useful, named test results.

Also run the advisory repository check:

```bash
python3 .github/scripts/check_core_standard.py
```

## Configure Classroom 50 consistently

The sample grading setup uses a cheap import guard followed by the pytest
suite:

```sh
python3 -c "import src.stats"
python3 -m pip install --quiet -r requirements.txt
python3 -m pytest -q tests/test_stats.py
```

Change `src.stats` and `tests/test_stats.py` if you rename them. The import
guard gives students a direct error when collection is broken; the pytest test
then awards points across the collected cases. See
[Writing tests with the CLI](writing-tests.md) or
[Writing tests with the Web UI](writing-tests-web.md) for the complete setup.

## Common Python adaptation problems

### pytest cannot import a module from `src`

Run tests from the repository root with `python3 -m pytest`, not by launching a
test file directly. Confirm that `src/__init__.py` exists and the import path
matches the filename exactly, including case on Linux.

### pytest collects zero tests

Use filenames such as `test_queue.py`, functions such as `test_fifo_order`, and
classes such as `TestQueue`. Check collection explicitly:

```bash
python3 -m pytest --collect-only -q
```

If the collection count changed intentionally, update `EXPECTED_CASES`.

### A dependency imports locally but fails in CI

The dependency is probably installed globally but missing from
`requirements.txt`, or it is unavailable for Python 3.12 on GitHub's Linux
runner. Recreate a virtual environment, install only `requirements.txt`, and
test there.

### A command works on one operating system only

Prefer `python3 -m module` form in shared shell instructions and `py -m module`
in Windows PowerShell instructions. Use `pathlib` in Python code instead of
hard-coded slash direction, and avoid depending on filename case differences.

### The template CI runs the full suite and turns red

On GitHub, mark the repository as a template under **Settings → General →
Template repository**. The workflow checks `github.event.repository.is_template`.
When that value is absent or false, it intentionally defaults to student mode
and runs all tests.

## Final adaptation checklist

- [ ] Student requirements name every required module and public interface.
- [ ] Unimplemented starter functions raise `NotImplementedError`.
- [ ] Imports have no interactive, network, or filesystem side effects.
- [ ] Tests use pytest discovery names and cover documented edge cases.
- [ ] `requirements.txt` contains every non-standard-library dependency.
- [ ] `python3 -m pytest --collect-only -q` finds the intended cases.
- [ ] `EXPECTED_CASES` matches the collection count.
- [ ] A correct solution passes and a deliberately wrong solution fails.
- [ ] Classroom 50 commands match the current module and test paths.
- [ ] README and student guides contain no stale instructions from another
      language or project layout.
