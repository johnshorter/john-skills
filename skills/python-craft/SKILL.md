---
name: python-craft
description: >
  Python craft for this lab: how we write, structure, and package Python so an analysis stays
  maintainable and reproducible. Use when writing or reviewing Python, setting up a Python
  project or environment, or porting analysis code to Python. For R, use the tidyverse and
  package skills. For teaching Python to students, use teaching-python.
---

# Python Craft

The Python counterpart to the lab's R skills. Write readable code first; optimize only when a
profiler says to.

## Environment and dependencies

One pinned environment per project. Never install into the base interpreter, never rely on
whatever is on `PATH`.

- **Pure Python, no compiled bioinformatics binaries**: use `uv`. Fast, one lockfile
  (`uv.lock`), `pyproject.toml` as the single source of truth.
- **Anything needing conda-only binaries** (bcftools, samtools, plink, and friends): use
  `mamba`/`conda`, one `environment.yml` per project, and export an exact lock.

LAB CALL: which of the two is the house default and when to switch. Commit the lockfile. Record
the Python version floor in `pyproject.toml` (`requires-python`).

## Project layout

Use a `src/` layout so imports match what gets installed:

```
project/
  pyproject.toml
  src/project/__init__.py
  src/project/...
  tests/
  scripts/        # entry points, thin wrappers over src/
  notebooks/      # exploration only, never the source of truth
```

Notebooks explore. Anything reused moves into `src/` and gets a test. A result that only
exists in a notebook cell is not reproducible.

## Data stack

- `numpy` for arrays, `pandas` as the default dataframe. Reach for `polars` when data is
  large or a pandas step is the bottleneck (lazy frames, real speed, no index surprises).
  LAB CALL: pandas-first or polars-first.
- Set dtypes explicitly on read (`dtype=`, `parse_dates=`). Use `category` for repeated
  strings. Never trust inferred types on a wide file.
- Vectorize. A `.apply` over rows or a Python `for` loop over a dataframe is almost always
  the wrong tool. If you wrote `df.iterrows()`, stop and reach for a vector op or a `groupby`.
- Prefer `parquet` over CSV for anything intermediate. It keeps dtypes and is faster.

## The decisions newcomers get wrong

The recurring traps live in [references/newcomer-traps.md](references/newcomer-traps.md).
Read it before reviewing a newcomer's first pull request. The short list: mutable default
arguments, aliasing versus copying, pandas chained assignment, `is` versus `==`, integer
and float surprises, path handling, unseeded randomness, and mutating a list while iterating
it.

## Correctness and testing

- `pytest`, small and fast. Test the data transforms, not the plumbing.
- For a transform, assert the invariant, not just one output: row counts preserved, no
  duplicate keys introduced, ranges sane, no unexpected nulls.
- Fixtures for tiny synthetic inputs. Do not test against a 40 GB file.
- Type hints at function boundaries and public APIs; run `mypy` or `pyright` there. Do not
  over-annotate trivial internals. Types are documentation that the checker enforces.

## Reproducibility

- Seed every RNG (`numpy.random.default_rng(seed)`, and pass generators explicitly rather
  than relying on global state).
- Log the versions that produced a result (`pip freeze` or the lockfile hash) alongside the
  output.
- Deterministic ordering: sort before you write, do not rely on dict or set iteration order
  for anything that lands in a file.

## Style

`ruff` for lint and format (Black-compatible, import sorting built in). Small functions,
American-English docstrings.

## Interop with R

If R calls this code, keep the handoff at a file boundary (parquet or CSV) or use
`reticulate` with a pinned env. Do not pass live objects across a language boundary in a
pipeline you expect to rerun.
