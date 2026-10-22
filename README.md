# NumPy 100 Solutions

![Python](https://img.shields.io/badge/python-3.9%2B-blue)
![NumPy](https://img.shields.io/badge/numpy-practice-013243)
![License: MIT](https://img.shields.io/badge/license-MIT-green)
![Progress](https://img.shields.io/badge/progress-10%2F100-orange)

My solutions to the [100 NumPy exercises](https://github.com/rougier/numpy-100) by Nicolas P. Rougier, written while learning NumPy. Each problem includes a commented solution plus a short note on the concept behind it.

## Goals
- Build real fluency with NumPy: indexing, broadcasting, vectorization, boolean masks, `axis` operations
- Write idiomatic, loop-free solutions
- Track which problems were hard and revisit them

## Progress

**Solved: 10 / 100**

| Problems | Notebook | Solved | Status |
|---|---|---|---|
| 1–10 | [`001-010.ipynb`](notebooks/001-010.ipynb) | 10/10 | ✅ |
| 11–20 | [`011-020.ipynb`](notebooks/011-020.ipynb) | 0/10 | ⬜ |
| 21–30 | [`021-030.ipynb`](notebooks/021-030.ipynb) | 0/10 | ⬜ |
| 31–40 | [`031-040.ipynb`](notebooks/031-040.ipynb) | 0/10 | ⬜ |
| 41–50 | [`041-050.ipynb`](notebooks/041-050.ipynb) | 0/10 | ⬜ |
| 51–60 | [`051-060.ipynb`](notebooks/051-060.ipynb) | 0/10 | ⬜ |
| 61–70 | [`061-070.ipynb`](notebooks/061-070.ipynb) | 0/10 | ⬜ |
| 71–80 | [`071-080.ipynb`](notebooks/071-080.ipynb) | 0/10 | ⬜ |
| 81–90 | [`081-090.ipynb`](notebooks/081-090.ipynb) | 0/10 | ⬜ |
| 91–100 | [`091-100.ipynb`](notebooks/091-100.ipynb) | 0/10 | ⬜ |

## Repository structure
```
numpy-100-solutions/
├── notebooks/        # one notebook per 10 problems
├── notes.md          # concepts learned and tricky problems
├── requirements.txt  # numpy + jupyterlab
├── LICENSE           # MIT (my work)
├── NOTICE.md         # attribution for the original problem set
└── README.md
```

## How I work through each problem
1. Attempt it alone for 10–15 minutes, printing `.shape` and `.dtype` often
2. Check the docs (`np.info(...)`, `help(...)`), then the hints
3. Look at the official solution only after trying
4. Rewrite it from memory and record the concept in the note cell
5. Revisit problems that needed help a few days later

Each problem ends with a note cell:
- **Concept:** the NumPy idea it practiced
- **Needed help?** no / hint / solution
- **Revisit on:** date to retry

## Setup
```bash
git clone https://github.com/tanjilhasanemon/numpy-100-solutions.git
cd numpy-100-solutions
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter lab
```

## Key takeaways so far
See [`notes.md`](notes.md).

## Credits
Problems are from [rougier/numpy-100](https://github.com/rougier/numpy-100) (MIT License); see [`NOTICE.md`](NOTICE.md). Solutions and notes are my own.

## License
[MIT](LICENSE)
