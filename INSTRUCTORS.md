# Instructor Guide

These labs were written as hands-on extensions to problem sets and quizzes in **API-232** at the Harvard Kennedy School. Each one revisits ideas students have already met on a homework or quiz, applies them to real NFL data, and finishes with a short written policy question.

This guide covers what each lab teaches, how long the parts take, what students need beforehand, and how to adapt the labs if you teach a different course.

## Format

* **One notebook per lab session**, 60–75 minutes, designed for Google Colab (see the [README](README.md) for links and local setup).
* Students fill in code cells marked with `...` / `TODO` comments and write short answers in markdown cells marked **✏️ Your answer**.
* Data-building and plotting cells are **provided**, so class time goes to the analysis rather than data cleaning.
* Each `*_SOLUTIONS.ipynb` notebook has the completed code and model written answers. Solutions are public in this repository.

## Prerequisites

Students should be comfortable with:

* Basic Python and `pandas` (filtering, `groupby`, computing means). No prior `nflreadpy` or football knowledge is assumed; each lab explains the football it uses.
* For the **OT** lab: means, standard errors, confidence intervals, z-tests.
* For the **Draft** lab: multiple regression and interpreting coefficients; ideally an introduction to double ML, omitted-variable bias and regression discontinuity.
* For the **Fantasy** lab: setting up a linear program (objective, constraints); ideally an introduction to matching mechanisms (Boston / deferred acceptance).

---

## Lab 1: Does getting the ball first win overtime? (`ot_lab/`, ~60 min)

**Big idea:** the overtime coin toss is a natural randomized experiment. Students check that randomization worked, estimate the first-possession advantage, ask whether the NFL's rule changes reduced it, and discover that the study has limited power to detect such changes.

| Part | Time | Content |
|---|---|---|
| 0. Setup | 3 min | Install `nflreadpy`; download play-by-play 1999–2025 one season at a time, keeping overtime plays (1–3 min download) |
| 1. Was the coin toss random? | 10 min | Balance on home field and pregame point spread |
| 2. How big is the advantage? | 15 min | Win share, SE, 95% CI, z-test, p-value; non-interference and why the two-group SE formula is wrong here |
| 3. Did the rule change work? | 15 min | Estimates by overtime era; difference between eras and its SE |
| 4. Could we have detected it? | 12 min | Power: rule-of-thumb, then simulation |
| 5. Significance vs. importance | 5 min | Written response |
| Extension (optional) | — | Mechanism: what happened on the first overtime drive under each set of rules |

**Data:** nflverse play-by-play, 1999–2025.

## Lab 2: Do NFL teams fall for the sunk-cost fallacy? (`draft_lab/`, ~75 min)

**Big idea:** first-round draft picks are expensive. If coaches give them more playing time than equally good later picks, that's the sunk-cost fallacy. The hard part, as in many policy evaluations, is that the expensive choices were also expected to be the best.

| Part | Time | Content |
|---|---|---|
| 0. Setup | 3 min | Download draft picks, snap counts and season stats; build a player-season panel (provided) |
| 1. Raw comparison | 8 min | Naive difference in playing time; balance on previous-season performance |
| 2. Adding controls | 15 min | Add control groups cumulatively and watch the coefficient (LaLonde-style); a bad control (this season's targets/carries) |
| 3. Double machine learning | 12 min | Random-forest DML with cross-fitting (`GroupKFold` by player); a "buggy" version without cross-fitting |
| 4. Sensitivity analysis | 10 min | Robustness value (Cinelli & Hazlett, 2020) |
| 5. Selecting on an outcome | 7 min | Restricting to players still in the league in year 4 |
| 6. Regression discontinuity | 15 min | Jump in early-career playing time at the round 1 / round 2 cutoff (pick 32/33) |
| 7. Bringing it together | 5 min | Written advice to a state budget office |

**Data:** nflverse draft picks, snap counts (2013–2025) and player season statistics (2013–2025). Analysis sample: WR, RB and TE drafted in rounds 1–3, 2013–2022, career years 2–4. The RD sample uses all positions except K/P/LS, drafted 2013–2021.

## Lab 3: Building a fantasy football team under a salary cap (`ff_lab/`, ~75 min)

**Big idea:** choosing a fantasy roster under a salary cap is a constrained optimization problem, like allocating a budget across programs. Students solve it, interpret binding constraints and shadow prices, see the optimizer's curse in real data, and compare waiver-wire matching mechanisms.

| Part | Time | Content |
|---|---|---|
| 0. Setup | 3 min | Download season stats and contracts; build a player pool with real salaries, projections and actual points (provided) |
| 1. Writing down the problem | 12 min | Objective and constraints for an 8-player roster under a $50M cap |
| 2. Solving it | 15 min | `scipy.optimize.milp`; value of more cap space; LP relaxation and shadow prices; "binding" in integer problems |
| 3. Adding rules | 10 min | "Spread the talent" and "veteran minimum" rules; the cost of a binding rule |
| 4. The optimizer's curse | 18 min | Projected vs. actual points; simulation with unbiased forecasts; calibrating forecasts on past seasons |
| 5. The waiver wire as a matching market | 12 min | Boston mechanism vs. deferred acceptance; stability and strategic reporting |
| 6. Bringing it together | 5 min | Written advice to a city housing agency |

**Data:** nflverse player season statistics (2013–2025) and OverTheCap contracts (via nflverse). Projections are deliberately naive (last season's points per game × 17).

---

## API-232 cross-references

The notebooks refer to specific API-232 assignments and quizzes so students can connect the labs to earlier work. If you teach a different course, these references won't mean anything to your students. Each one is listed below with what it refers to, so you can point to your own equivalent or delete the sentence.

| Lab | Reference in the notebook | What it refers to | Substitute |
|---|---|---|---|
| OT | "Concepts from Quiz 4" | A quiz on randomized experiments, SEs, CIs, significance, power and non-interference | Your unit on experiments |
| OT | "Quiz 4, Question 2(d)", the coaching example | A question about bias from differences between treatment and control groups | Any balance / selection example |
| OT | "the Quiz 4 formula SE = √(s²ₜ/nₜ + s²꜀/n꜀)" | Standard two-sample SE for a difference in means | Self-explanatory; keep as is |
| OT | "the Quiz 4 rule of thumb" | Significance needs an estimate ≈ 2 × SE from zero; 80% power needs ≈ 2.8 × SE | Self-explanatory; keep as is |
| Draft | "Concepts from Assignment 5" | A problem set on causal inference with observational data | Your unit on observational causal inference |
| Draft | "the LaLonde problem" (Assignment 5, Problem 2) | LaLonde (1986) NSW job-training data, comparing experimental results with CPS comparison groups | LaLonde is widely taught; any selection-on-observables example works |
| Draft | `dml_buggy.py` (Assignment 5, Problem 2) | A DML script with a cross-fitting bug | Any DML introduction |
| Draft | "birth-weight paradox" (Assignment 5, Problem 3) | Conditioning on a post-treatment / collider variable | Any bad-control or collider example |
| Draft | "Problem 4 (tariffs)" | A regression discontinuity exercise | Any RD example |
| Draft | "randomizing households instead of individuals in Quiz 4" | Cluster randomization and clustered SEs | Any clustering example |
| Fantasy | "Concepts from Quiz 3", "Quiz 3's vaccination drive" | A linear program allocating vaccination station-hours, with a rule requiring at least 50 mobile-van hours | Any budget-allocation LP |
| Fantasy | "the summer-jobs question on the quiz" (Question 3) | Boston mechanism vs. deferred acceptance for assigning students to summer jobs | Any school-choice / matching example |
| Fantasy | "fractional station-hours" | The quiz LP allowed continuous variables | Explain LP vs. integer programming directly |

## Adapting the labs

* **Timing:** each part has a time estimate in its heading. To fit a shorter session, drop the optional OT extension, Draft Part 5, or Fantasy Part 5; each is self-contained.
* **Seasons:** season ranges are set in the provided setup cells (e.g. `range(1999, 2026)`). Extend them as nflverse adds new seasons; some written answers in the solutions quote specific numbers that will shift.
* **Data changes:** nflverse occasionally renames columns. If a setup cell fails, check the [nflreadpy documentation](https://nflreadpy.nflverse.com/) and the column names in the downloaded table.
* **Colab memory:** the OT lab downloads play-by-play one season at a time and keeps only overtime plays to stay within Colab's free tier. Avoid loading all seasons at once.
* **Grading:** written answers are in clearly marked cells, so students can submit the notebook (`.ipynb`) or a PDF export.

## Feedback

Corrections and suggestions are welcome as GitHub issues or pull requests.
