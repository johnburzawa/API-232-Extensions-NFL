# API-232 Extensions: NFL Labs

Three self-contained Python labs that teach core quantitative-methods ideas — randomized experiments, causal inference with observational data, and constrained optimization — using free, real NFL data. They were written as extensions for **API-232** at the Harvard Kennedy School, and every lab ends by carrying the lesson over to a public-policy setting.

Each lab is a Jupyter notebook designed to run in **Google Colab** in a single 60–75 minute session, with a matching **solutions** notebook for instructors.

| Lab | Question | Methods | Time |
|---|---|---|---|
| [OT Coin Toss](ot_lab/) | Does getting the ball first win overtime? | Randomized experiments, balance checks, proportions, CIs and hypothesis tests, statistical power by simulation, significance vs. practical importance | ~60 min |
| [Draft Sunk Cost](draft_lab/) | Do NFL teams fall for the sunk-cost fallacy? | Confounding and controls (LaLonde-style), bad controls, double machine learning with cross-fitting, sensitivity analysis (robustness value), selection on outcomes, regression discontinuity | ~75 min |
| [Fantasy Optimization](ff_lab/) | How do you build the best fantasy team under a salary cap? | Integer and linear programming, binding constraints and shadow prices, the optimizer's curse, forecast calibration, matching markets (waiver wire) | ~75 min |

A suggested order is **OT → Draft → Fantasy**, but each lab stands alone.

## Running the labs

### Option 1: Google Colab (recommended, nothing to install)

Click a badge to open the student notebook:

| Lab | Student notebook | Solutions |
|---|---|---|
| OT Coin Toss | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/johnburzawa/API-232-Extensions-NFL/blob/main/ot_lab/OT_Coin_Toss_Lab.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/johnburzawa/API-232-Extensions-NFL/blob/main/ot_lab/OT_Coin_Toss_Lab_SOLUTIONS.ipynb) |
| Draft Sunk Cost | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/johnburzawa/API-232-Extensions-NFL/blob/main/draft_lab/Draft_Sunk_Cost_Lab.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/johnburzawa/API-232-Extensions-NFL/blob/main/draft_lab/Draft_Sunk_Cost_Lab_SOLUTIONS.ipynb) |
| Fantasy Optimization | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/johnburzawa/API-232-Extensions-NFL/blob/main/ff_lab/Fantasy_Optimization_Lab.ipynb) | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/johnburzawa/API-232-Extensions-NFL/blob/main/ff_lab/Fantasy_Optimization_Lab_SOLUTIONS.ipynb) |

Colab opens a read-only copy. Students should choose **File → Save a copy in Drive** before they start writing answers. Then run the cells from the top; the first cell installs [`nflreadpy`](https://github.com/nflverse/nflreadpy) and downloads the data (1–3 minutes).

### Option 2: Run locally

Requires Python 3.10 or newer.

```bash
git clone https://github.com/johnburzawa/API-232-Extensions-NFL.git
```

```bash
cd API-232-Extensions-NFL
```

```bash
python3 -m venv .venv && source .venv/bin/activate
```

```bash
pip install -r requirements.txt
```

```bash
jupyter lab
```

The notebooks' first cell runs `!pip install -q nflreadpy`; this is harmless locally once the requirements are installed.

All three solution notebooks were last run end to end in November 2026 with Python 3.14, nflreadpy 0.1.5, pandas 3.1, numpy 2.5, scipy 1.18, statsmodels 0.15, scikit-learn 1.9 and polars 2.1.

## Data

All data comes from the free, open [nflverse](https://github.com/nflverse) project via `nflreadpy` and is downloaded at runtime; nothing is stored in this repository. An internet connection is required.

| Lab | Tables used |
|---|---|
| OT Coin Toss | Play-by-play, 1999–2025 (only overtime plays are kept, one season at a time, to fit in Colab's memory) |
| Draft Sunk Cost | Draft picks, snap counts (2013–2025), player season statistics (2013–2025) |
| Fantasy Optimization | Player season statistics (2013–2025), contracts (from OverTheCap, via nflverse) |

Because nflverse updates its data during the season, numbers you get may differ slightly from those quoted in the solutions, especially for the most recent season.

## Repository layout

```
ot_lab/      OT_Coin_Toss_Lab.ipynb            + _SOLUTIONS.ipynb
draft_lab/   Draft_Sunk_Cost_Lab.ipynb         + _SOLUTIONS.ipynb
ff_lab/      Fantasy_Optimization_Lab.ipynb    + _SOLUTIONS.ipynb
INSTRUCTORS.md   Learning goals, timing, course cross-references, adaptation tips
requirements.txt Packages for running locally
```

## For instructors

See **[INSTRUCTORS.md](INSTRUCTORS.md)** for learning objectives, prerequisites, a part-by-part timing guide, the API-232 course materials the labs refer to (and what to substitute if you teach elsewhere), and tips for adapting them.

Solutions are public by design. If you're assigning the labs for credit, consider that students can find them here.

## License

* Teaching content (notebook text, questions, solutions and documentation): [Creative Commons Attribution 4.0 (CC BY 4.0)](LICENSE-CONTENT.md)
* Code: [MIT License](LICENSE)

You're welcome to use, adapt and redistribute these labs, including in your own courses, with attribution.

NFL data is provided by [nflverse](https://github.com/nflverse) under its own terms; contract data originates from [OverTheCap](https://overthecap.com). This project is not affiliated with or endorsed by the NFL.

## Citation

> Burzawa, J. *API-232 Extensions: NFL Labs.* Harvard Kennedy School, 2026. https://github.com/johnburzawa/API-232-Extensions-NFL
