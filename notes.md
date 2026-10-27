# Notes

Short takeaways while solving. One line per concept is enough.

## Concepts learned

### Problems 1–10
- **Aliasing:** `import numpy as np` is the universal convention.
- **Default dtype:** `np.zeros` / `np.ones` give `float64` unless `dtype=` is set.
- **Memory:** `nbytes == size * itemsize`; smaller dtypes use less memory.
- **Docs habit:** `np.info(f)`, `help(f)`, and `f?` in Jupyter.
- **Indexing:** 0-based; assign with `Z[i] = value`.
- **`arange`:** the stop value is exclusive, like Python's `range`.
- **Views vs copies:** slices such as `Z[::-1]` are views and share memory with the original.
- **`reshape`:** needs the same total number of elements; fills row by row.
- **`nonzero`:** returns a tuple of index arrays, one per dimension.

### Problems 11–20
- **Identity / diagonals:** `np.eye(n)`; `np.diag(v, k)` places `v` on the k-th diagonal (negative k is below the main one).
- **Random numbers:** `rng = np.random.default_rng(seed)`, then `rng.random(shape)`; seeding makes results reproducible.
- **Reductions:** `.min()`, `.max()`, `.mean()`; `argmin`/`argmax` give flat positions, `np.unravel_index` turns them into (row, col).
- **Slice assignment:** `Z[1:-1, 1:-1] = 0` edits the interior; `Z[1::2, ::2]` uses steps for patterns like a checkerboard.
- **Padding:** `np.pad(Z, 1, mode="constant", constant_values=0)` adds a border on every side.
- **NaN and floats:** `nan != nan`, comparisons with `nan` are False, so use `np.isnan`; compare floats with `np.isclose`, never `==`.
- **Flat vs multi-dim index:** the 100th element has flat index 99; `np.unravel_index(99, shape)` gives its coordinates.

### Problems 21–25
- **`np.tile`:** repeats a small block; a 2x2 block tiled `(4, 4)` gives an 8x8 checkerboard.
- **Normalization:** z-score `(Z - Z.mean()) / Z.std()` or min-max `(Z - Z.min()) / (Z.max() - Z.min())`; both rely on broadcasting.
- **Structured dtypes:** `np.dtype([("r", np.ubyte), ...])` gives named fields per element; read one with `arr["r"]`.
- **Matrix product:** `A @ B` / `np.dot(A, B)` needs matching inner dimensions; `*` is element-wise.
- **Boolean masks:** combine with `&` / `|` and parentheses, never `and` / `or`; `Z[mask] *= -1` edits in place.

### Problems 26–30
- **Built-in vs NumPy `sum`:** `sum(x, -1)` starts counting from -1; `np.sum(x, -1)` sums along the last axis. Avoid `from numpy import *`, which shadows built-ins.
- **Operator parsing:** `Z <- Z` is `Z < (-Z)`; chained comparisons like `Z<Z>Z` fail on arrays because `and` needs a single True/False.
- **Division by zero:** `0/0` is `nan`; integer `0//0` is `0` (both with warnings); casting `nan` to int is platform dependent.
- **Rounding away from zero:** `np.where(Z > 0, np.ceil(Z), np.floor(Z))`; `np.round` rounds to nearest instead.
- **Common values:** `np.intersect1d(a, b)` for sorted unique matches; `np.isin(a, b)` for a boolean mask.

## Tricky problems (revisit)
| # | Why it was tricky | Revisit date |
|---|---|---|
| 5 | Remembering how to look up docs | Oct 24 |
| 7 | Exclusive stop in `arange` | Oct 24 |
| 8 | Reverse is a view, not a copy | Oct 24 |
| 9 | `reshape` shape must match size | Oct 24 |
| 10 | `nonzero` returns a tuple | Oct 24 |
| 15 | Interior slice `1:-1` | Oct 26 |
| 16 | Remembering `np.pad` and its arguments | Oct 26 |
| 17 | NaN rules and float comparison | Oct 26 |
| 18 | `np.diag` with `k` offset | Oct 26 |
| 19 | Step slicing for the checkerboard | Oct 26 |
| 20 | Flat index 99, not 100 | Oct 26 |
| 21 | Choosing the right block and reps for `np.tile` | Oct 29 |
| 22 | Two meanings of "normalize" | Oct 29 |
| 23 | Structured dtype syntax | Oct 29 |
| 25 | `&` with parentheses for masks | Oct 29 |
| 26 | Built-in `sum` vs `np.sum` with `-1` | Oct 31 |
| 27 | Operator precedence and chained comparisons | Oct 31 |
| 28 | Division by zero and nan-to-int casts | Oct 31 |
| 29 | Rounding away from zero vs `np.round` | Oct 31 |
| 30 | `intersect1d` vs `isin` | Oct 31 |

## Idiomatic tricks I want to remember
- Prefer vectorized operations and slicing over Python loops
- Print `.shape` and `.dtype` whenever the result looks wrong
