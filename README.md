# SemProject_MLEngine: Njia stop finder (ICS 3202)

**Group:** Aaron, Bradley, Kate

Njia helps matatu riders in Nairobi. Its machine-learning feature, the stop finder, takes the stop name a rider types, even with typos or shortened names, and finds the stop they meant on route 125 (Ongata Rongai – Railways/CBD). When it isn't sure, it says so.

## Files
| File | What it is |
|---|---|
| `DigitalMatatusNairobi_Exploration.ipynb` | Deliverable 1: first exploration of the Digital Matatus data |
| `LogisticRegression_Base.ipynb` | Deliverable 2, the base model: data cleaning, EDA and the four name features, as presented. |
| `LogisticRegression_Final.ipynb` | Deliverable 3, the final ML engine: data → cleaning → EDA → features → cross-validation → logistic regression → validation → cutoff → test → comparison with an exact/fuzzy rule and a pretrained model → explanation → saved model → limitations |
| `Bradley_Reviewed_Data_v1.zip`, `cleaning_log_v1.csv` | The reviewed dataset the notebooks use |
| `mdb-1815-202406071505.zip` | The 2019 Digital Matatus GTFS feed (Mobility Database mdb-1815). The Final notebook downloads it if it's missing. |
| `app/` | The demo app: a phone-sized web app that loads the model exported by the Final notebook. |

## How the engine works
For every stop on route 125, the engine compares it with what the rider typed using four measures: exact match, how many letters line up (Levenshtein similarity), how many words are shared, and how different the lengths are. A logistic regression model, trained on our labelled examples, combines these into a score from 0 to 1. The app only answers when the best stop scores at least 0.476 (a cutoff chosen on validation data) and no other stop ties with it. Otherwise it says "not sure" or "no confident match". A "Why this?" panel shows the rider how much each measure pushed the score up or down.

## Results (right stop alone at the top, 21 searches per split)
| Method | Validation | Test |
|---|---|---|
| Exact match, then fuzzy (rule) | 19/21 | 21/21 |
| **Logistic regression (used in the app)** | 20/21 | 21/21 (pair precision 0.83, recall 0.95) |
| Pretrained multilingual-E5-small, no training | 21/21 | 20/21 |

On ranking, the three are about level. Logistic regression is used in the app because its scores separate real matches from nonsense, which makes "no confident match" possible, and because it can explain itself and runs offline on a phone.

## Run the Final notebook
Open `LogisticRegression_Final.ipynb` in Colab or Jupyter, with `Bradley_Reviewed_Data_v1.zip`, `cleaning_log_v1.csv` and (optionally) `mdb-1815-202406071505.zip` in the same folder, then Run all. To compute the test results, set `ICS3202_RUN_HELD_OUT=1` first (the notebook's first cell does this). The notebook also writes `ics3202_outputs/Kate_Model_Handoff.zip`, which the app loads.

## Limitations
- The 94 test searches were written by the team, not real riders, and each split has only 21 of them.
- The engine knows only route 125's 78 stops (62 place names) and compares spelling only. A real place elsewhere that is spelled like a route stop (e.g. "kencom" → Kenol) can get a confident wrong answer.

## Data and credits
- Stop data: Digital Matatus 2019 GTFS feed, via the Mobility Database (mdb-1815). Used with permission.
- Fonts in the app: Bricolage Grotesque and Plus Jakarta Sans (SIL Open Font License; licence files in `app/static/licenses`).
