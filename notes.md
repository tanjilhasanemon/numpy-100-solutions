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

## Tricky problems (revisit)
| # | Why it was tricky | Revisit date |
|---|---|---|
| 5 | Remembering how to look up docs | Oct 24 |
| 7 | Exclusive stop in `arange` | Oct 24 |
| 8 | Reverse is a view, not a copy | Oct 24 |
| 9 | `reshape` shape must match size | Oct 24 |
| 10 | `nonzero` returns a tuple | Oct 24 |

## Idiomatic tricks I want to remember
- Prefer vectorized operations and slicing over Python loops
- Print `.shape` and `.dtype` whenever the result looks wrong
