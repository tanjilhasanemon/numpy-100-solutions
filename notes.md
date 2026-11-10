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

### Problems 31–35
- **Warnings:** `np.seterr(all="ignore")` is global and returns the old settings; prefer `with np.errstate(...)` for a single block.
- **Real vs complex sqrt:** `np.sqrt(-1)` is `nan`; `np.emath.sqrt(-1)` is `1j`; `nan == 1j` is False.
- **Dates:** `np.datetime64("today")` plus or minus `np.timedelta64(n, "D")`.
- **Date ranges:** `np.arange("2016-07", "2016-08", dtype="datetime64[D]")` lists every day of July (stop is exclusive).
- **In-place math:** ufuncs take `out=` (`np.add(A, B, out=B)`) so no temporary arrays are created; arrays must be float for in-place division.

### Problems 36–40
- **Integer part:** `Z - Z % 1`, `np.floor`, `astype(int)`, `np.trunc` agree for positives; floor and trunc differ for negatives.
- **Row broadcasting:** `Z += np.arange(5)` adds a length-5 row to every row of a 5x5 array.
- **Generators:** `np.fromiter(gen, dtype=int, count=n)` builds an array without making a list; `np.array(gen)` does not work.
- **Open interval:** `np.linspace(0, 1, 11, endpoint=False)[1:]` gives 10 values strictly between 0 and 1.
- **Sorting:** `np.sort(Z)` returns a copy, `Z.sort()` sorts in place, `argsort` returns indices, `[::-1]` reverses.

### Problems 41–50
- **Small-array speed:** `np.add.reduce(Z)` skips the `np.sum` wrapper overhead; measure with `timeit`.
- **Equality checks:** `np.array_equal` is strict (shape and values); `np.allclose` uses a tolerance and broadcasts.
- **Read-only arrays:** `Z.flags.writeable = False` makes writes raise `ValueError`.
- **Polar coordinates:** `r = np.hypot(x, y)`, `theta = np.arctan2(y, x)` (handles all quadrants).
- **Replace the max:** `Z[Z.argmax()] = 0` changes the first max only; `Z[Z == Z.max()] = 0` changes all.
- **Structured grids:** `np.meshgrid` plus a structured dtype with `x` and `y` fields covers [0,1]x[0,1].
- **Outer ufuncs:** `np.subtract.outer(X, Y)` builds all pairwise differences; `1 / that` is the Cauchy matrix.
- **Type limits:** `np.iinfo(dtype)` and `np.finfo(dtype)` give min, max and eps.
- **Printing everything:** `with np.printoptions(threshold=sys.maxsize):` prints the full array.
- **Closest value:** `Z[np.abs(Z - z).argmin()]`.

### Problems 51–60
- **Nested structured dtypes:** a field can hold another list of fields; access with `Z["position"]["x"]`.
- **Pairwise distances:** broadcast a column against a row: `X[:, None] - X[None, :]`, then `sqrt(dx² + dy²)`.
- **In-place type conversion:** `Y = Z.view(np.int32); Y[:] = Z` converts float32 to int32 without a new buffer.
- **Reading messy text:** `np.genfromtxt(f, delimiter=",")` handles blanks (nan, or -1 for `dtype=int`).
- **enumerate for arrays:** `np.ndenumerate(Z)` gives `(index, value)`; `np.ndindex(shape)` gives indices only.
- **Gaussian grid:** `meshgrid` for coordinates, then `np.exp(-(d - mu)**2 / (2 * sigma**2))`.
- **Random placement:** `rng.choice(n*n, p, replace=False)` for unique positions, then `np.put`.
- **Row-wise operations:** `X - X.mean(axis=1, keepdims=True)`; `keepdims` keeps the shape broadcastable.
- **Sort rows by a column:** `Z[Z[:, n].argsort()]`.
- **Null columns:** `~Z.any(axis=0)` marks all-zero columns.

### Problems 61–70
- **Nearest value:** `Z[np.abs(Z - z).argmin()]`; use `.flat` for multi-dimensional arrays.
- **Iterators:** `np.nditer([A, B, None])` broadcasts arrays together and can allocate the output.
- **Subclassing ndarray:** create with `__new__` and `.view(cls)`; copy attributes in `__array_finalize__`.
- **Repeated indices:** `Z[I] += 1` counts repeats once; use `np.bincount(I, minlength=n)` or `np.add.at(Z, I, 1)`.
- **Accumulating by index:** `np.bincount(I, weights=X)` sums `X` per index.
- **Counting colors:** `np.unique(img.reshape(-1, 3), axis=0)`, or encode RGB into one integer (cast to `uint32` first to avoid overflow).
- **Multiple axes:** `A.sum(axis=(-2, -1))` reduces the last two axes at once.
- **Grouped means:** `np.bincount(S, weights=D) / np.bincount(S)`.
- **Diagonal of a product:** `np.einsum("ij,ji->i", A, B)` skips the full matrix product.
- **Interleaving zeros:** `Z0[::nz + 1] = Z` on a zero array of the right length.

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
| 31 | `seterr` vs `errstate` | Nov 3 |
| 32 | Real `sqrt` returns nan, `emath` returns complex | Nov 3 |
| 34 | Date ranges with `datetime64[D]` | Nov 3 |
| 35 | Chaining ufuncs with `out=` | Nov 3 |
| 36 | Floor vs trunc vs astype for integer part | Nov 8 |
| 38 | `np.fromiter` needs a dtype | Nov 8 |
| 39 | Excluding both ends with `linspace` | Nov 8 |
| 41 | Why `np.add.reduce` beats `np.sum` on small arrays | Nov 10 |
| 42 | `array_equal` vs `allclose` | Nov 10 |
| 43 | Read-only flag | Nov 10 |
| 44 | `arctan2` vs `arctan` | Nov 10 |
| 46 | Structured array with `meshgrid` | Nov 10 |
| 47 | `ufunc.outer` | Nov 10 |
| 48 | `iinfo` vs `finfo` | Nov 10 |
| 49 | `printoptions` threshold | Nov 10 |
| 51 | Nested structured dtype syntax | Nov 12 |
| 52 | Broadcasting for pairwise distances | Nov 12 |
| 53 | `view` + slice assignment for in-place cast | Nov 12 |
| 54 | `genfromtxt` and missing values | Nov 12 |
| 56 | Gaussian formula on a meshgrid | Nov 12 |
| 57 | `choice(replace=False)` + `np.put` | Nov 12 |
| 58 | Why `keepdims=True` matters | Nov 12 |
| 59 | `argsort` on one column, reindex rows | Nov 12 |
| 62 | `nditer` with an allocated output | Nov 15 |
| 63 | `__new__` and `__array_finalize__` | Nov 15 |
| 64 | Why `Z[I] += 1` ignores repeats | Nov 15 |
| 65 | `bincount` with `weights` | Nov 15 |
| 66 | Counting unique colors without overflow | Nov 15 |
| 67 | Tuple of axes in `sum` | Nov 15 |
| 68 | Grouped mean with `bincount` | Nov 15 |
| 69 | `einsum` for the diagonal of a product | Nov 15 |
| 70 | Step-slice assignment | Nov 15 |

## Idiomatic tricks I want to remember
- Prefer vectorized operations and slicing over Python loops
- Print `.shape` and `.dtype` whenever the result looks wrong
