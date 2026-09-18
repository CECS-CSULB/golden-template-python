# [Assignment Title]

<!--
FACULTY: This is the student-facing assignment guide. Replace every
placeholder in square brackets before distributing the repository. Remove any
sections that do not apply to your assignment.
-->

## Overview

<!-- FACULTY: Describe the problem students are solving, why it matters, and
what they are expected to build. Avoid putting grading-only details here. -->

In this assignment, you will [describe the program, library, or system the
student will implement]. The completed project should [summarize the main
result or behavior].

This assignment is intended to help you practice:

- [Learning objective 1]
- [Learning objective 2]
- [Learning objective 3]

## What you need to implement

<!-- FACULTY: List the files, functions, classes, or other artifacts students
are responsible for. Keep names and signatures exact. -->

| File or path | Required work |
|---|---|
| `src/[module].py` | [Function, class, or feature to implement] |
| `src/[another_module].py` | [Function, class, or feature to implement] |

Do not change [function names, signatures, public interfaces, or other
constraints]. You may create additional helper functions or files if [state
whether this is allowed].

## Requirements

<!-- FACULTY: State functional requirements and important edge cases. Be
specific enough that students can test their work locally. -->

Your solution must:

1. [Requirement 1]
2. [Requirement 2]
3. [Requirement 3]

Important edge cases include:

- [Edge case 1 and expected behavior]
- [Edge case 2 and expected behavior]
- [Edge case 3 and expected behavior]

## Input and output

<!-- FACULTY: Use this section for command-line programs. For library
assignments, replace it with the API contract and examples. -->

### Input

[Describe the input format, valid values, number of values, and termination
conditions.]

### Output

[Describe the required output, including labels, ordering, precision, and
whether additional output is allowed.]

Example:

```text
[Example input]
```

```text
[Expected output]
```

## Project layout

| Path | Purpose |
|---|---|
| `src/` | Importable starter and implementation modules |
| `src/__init__.py` | Marks `src` as a Python package |
| `tests/` | Public pytest test cases |
| `requirements.txt` | Python runtime and test dependencies |
| `docs/student/setup.md` | Python environment and local test instructions |
| `.github/workflows/ci.yml` | Automated checks run after pushes and pull requests |

Read [the setup guide](docs/student/setup.md) before installing dependencies or
running the tests.

## Test cases and grading

Your solution is checked with automated tests. The public test cases are
described below.

<!--
FACULTY: Replace this table with the tests in tests/. List one row per
meaningful test case or test group. Do not claim that a test is public if it is
hidden. If Classroom 50 or another grading system applies different weights,
make the authoritative weights clear in the course assignment instructions.
-->

| Test case | What it checks | Input or setup | Expected behavior | Points |
|---|---|---|---|---:|
| `[test_name_1]` | [Behavior being tested] | [Input or setup] | [Expected result] | [N] |
| `[test_name_2]` | [Behavior being tested] | [Input or setup] | [Expected result] | [N] |
| `[test_name_3]` | [Behavior being tested] | [Input or setup] | [Expected result] | [N] |
| **Total** |  |  |  | **[Total points]** |

The tests may check normal inputs, boundary conditions, invalid inputs, and
whether your implementation preserves required input data. Passing a sample
input alone is not sufficient; your implementation must satisfy the complete
contract above.

<!-- FACULTY: Choose and describe the applicable grading workflow. -->

Install the dependencies and run the tests locally with:

```bash
python3 -m pip install -r requirements.txt
python3 -m pytest -q
```

On Windows PowerShell, use:

```powershell
py -3.12 -m pip install -r requirements.txt
py -3.12 -m pytest -q
```

Continuous integration runs the configured checks after you push your work to
GitHub. If this assignment uses Classroom 50, its assignment settings determine
when a submission is graded and how test results are weighted.

## Submission checklist

Before submitting, confirm that:

- [ ] Your implementation is complete.
- [ ] All required modules import successfully.
- [ ] All local tests pass.
- [ ] Your input and output follow the required format, if applicable.
- [ ] You did not commit caches, secrets, or unrelated files.
- [ ] You completed any required course verification or AI-use log.

<!-- FACULTY: Add assignment-specific submission instructions, due dates,
branch/tag requirements, collaboration rules, and AI-use requirements here. -->

## Questions and help

<!-- FACULTY: Add the approved help channels and collaboration boundaries. -->

For questions, use [the course help channel or forum]. When asking for help,
include the command you ran, the relevant error message, and a minimal example
that reproduces the problem. Do not post private tokens or other sensitive
information.
