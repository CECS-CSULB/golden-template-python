# Guidance for Faculty

This template contains a small Python package and a `pytest` test suite. It
integrates with GitHub Actions so that every push to GitHub checks the project.
It can be used with Classroom 50 as the basis for an auto-graded programming
assignment, or given to students to fork by hand when auto-grading is not
needed.

The [faculty documentation](docs/faculty/README.md) explains how to adapt the
starter code, write tests, and optionally configure a Classroom 50 instance.
Before publishing an assignment to students, remove `docs/faculty` and this
faculty section if they would cause confusion.

## Faculty To-Do

1. Replace the sample statistics exercise in `src/` with the assignment's
   starter code.
2. Replace the tests in `tests/` and update `EXPECTED_CASES` in
   [`.github/workflows/ci.yml`](.github/workflows/ci.yml) if the number of test
   cases changes.
3. Edit [STUDENT_README.md](STUDENT_README.md) with the assignment requirements
   and review the guides linked from
   [docs/student/README.md](docs/student/README.md).
4. Add runtime and test dependencies to
   [requirements.txt](requirements.txt). Keep only packages the assignment
   actually needs.
5. Review the warning below and decide whether to keep the student publishing
   guide.
6. Read the [faculty documentation](docs/faculty/README.md) to understand the
   repository layout, CI commands, and optional Classroom 50 integration.
7. Create a GitHub template repository for the assignment, if needed.
8. If AI assistance is allowed, review or adapt the root
   [Verification Log](VERIFICATION-LOG.md); a clean faculty copy is available
   at [docs/faculty/VERIFICATION-LOG.md](docs/faculty/VERIFICATION-LOG.md).
   Otherwise, remove assignment-specific verification-log requirements.
9. Remove faculty-only documentation, then commit and push the assignment.

## Language-specific notes

This template targets Python 3.12 in CI and uses
[pytest](https://docs.pytest.org/) for testing. Dependencies are declared in
[`requirements.txt`](requirements.txt) and installed with:

```bash
python3 -m pip install -r requirements.txt
```

Project layout:

- Assignment logic lives in [`src/stats.py`](src/stats.py). Replace this sample
  module with the files for your assignment while keeping `src/` importable.
- [`src/__init__.py`](src/__init__.py) marks `src` as a package.
- Tests live in [`tests/test_stats.py`](tests/test_stats.py) and run with
  `python3 -m pytest -q`.
- The starter functions raise `NotImplementedError`. Keep that pattern for
  unfinished work: a bare `pass` silently returns `None` and makes an
  unimplemented function look like an incorrect implementation.
- [`.github/workflows/ci.yml`](.github/workflows/ci.yml) only verifies test
  collection in a template repository, because the starter is intentionally
  incomplete. A student copy runs the full suite.

Python discovers modules from the repository root, so new modules under `src/`
do not need to be registered in a build file. If you rename modules or tests,
update their imports, the CI commands, and the Classroom 50 grading commands
together.

## Warning about student documentation

The file [docs/student/publishing.md](docs/student/publishing.md) walks students
through publishing an approved copy of their completed assignment to a public
GitHub profile. It tells them to wait until the semester is over, obtain the
instructor's permission, and remove private course material first.

If students should not publish completed work, replace that guide with the
course's policy. Consider explaining how students may describe the work on a
résumé or portfolio without releasing the source.

# Guidance for Students

This assignment is derived from the CSULB CECS Department Golden Template, a
starting point for faculty to create programming assignments that use a
repeatable project layout, automated tests, and continuous integration.

Read [STUDENT_README.md](STUDENT_README.md) first for the assignment
requirements. Then use [docs/student/README.md](docs/student/README.md) for
setup, Git, development, README-writing, and publishing guides.
