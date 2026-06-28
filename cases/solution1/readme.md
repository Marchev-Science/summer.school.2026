# Longevity & the Labour Market — balancing supply and demand to 2033

[video](https://www.youtube.com/playlist?list=PLX9ryRl9v7BDRkeU63mUMS0ujziussz82)

### Team **Primus** — solution to the Marchev-Science summer-school case

**Authors:** Kalina Vladimirova · Hanna Velykova · Elena Dimitrova-Tsoleva · Rositsa Nikolova

---

## The case, in one sentence
For 8 European countries (Bulgaria, Poland, Czechia, Romania, Germany, France,
Norway, Switzerland), by sex, can each economy still **supply the labour its jobs
need by 2033** — and where does that balance break?

## Our solution — a person-year engine
You cannot weigh a life-expectancy number against a job vacancy: different units.
So we convert demographic averages into **one common currency, human-working-years**:

| Quantity | Definition |
|---|---|
| **Supply** | healthy working-age people × expected working life  =  `pop_15_64 × (HLY/LE) × working_life` |
| **Demand** | jobs (employed + vacancies) × required length of service |
| **Balance** | **Supply − Demand** |

Each *rate* driver is forecast to 2033 by a small **ensemble of five simple models**
(linear, damped Holt, drift, naive, AR(1)) with per-horizon weights and Monte-Carlo
uncertainty — **deliberately no neural networks**, because on ~13-21 years of data
flexible models overfit. **Population** uses Eurostat's official projection.

## Key results (reproduced live by the notebook)
- **Roughly balanced in aggregate, structurally divided.** Net balance ~ **+77 M**
  human-working-years, hiding an **East surplus ~ +383 M** (PL, RO, CZ, BG) against a
  **West/EFTA shortage ~ -306 M** (DE, FR, CH, NO) — the demographic basis of
  West-bound migration.
- **The longevity dividend holds the line:** working-age populations shrink, yet
  supply stays near-flat because people are healthier, work longer, and participate more.
- **Three policy levers** move the balance: increase supply, ease demand, maintain balance.
- **Validation (rolling-origin backtest, MAPE):** life expectancy **1.2 %**, working
  life **1.8 %**, employment **2.0 %**, healthy share **3.1 %**; job vacancies are a
  near-random-walk (~24-28 %) and are flagged honestly. The balance is a small
  difference of two large forecasts, so we read it as a **direction with wide bands**.

The notebook produces three charts: (1) the supply / demand / balance trajectory to
2033, (2) the 2033 balance by country (East surplus vs West shortage), and (3) the
validation error by driver.

> The full repository refines vacancies with an anchored Beveridge model and adds
> migration scenarios, bootstrap confidence intervals, CRPS scoring, and Levels 4-6
> (health-cost, retirement dividend, macroeconomy); its refined headline is net
> **+89 M** / East **+369 M** / West **-280 M** — the same qualitative conclusion.

## How to run
**Google Colab (recommended, zero setup):** upload `longevity_labour_market.ipynb`,
then *Runtime > Run all*. It installs its own libraries and downloads the public
input data — only an internet connection is required. Runs identically on any OS.

**Locally:** `pip install -r requirements.txt`, then open the notebook in Jupyter and
run all cells (Python 3.9+).

## Data sources (public, Eurostat)
`demo_pjan`, `proj_23np` (population & projection) · `hlth_hlye` (life expectancy &
healthy life years) · `lfsi_dwl_a` (duration of working life) · `lfsa_egan`
(employment) · `jvs_q_r21`, `une_rt_a` (vacancies & unemployment) · required length of
service from the case brief / MISSOC / OECD. The notebook downloads the harmonised
tidy panel and the official working-age population projection; the harmonisation
pipeline is documented in the full repository.

## Requirements
See `requirements.txt` (pandas, numpy, statsmodels, matplotlib, pyarrow, requests).
The notebook is **self-contained** — its first cell pip-installs these itself, so it
is independent of the operating system.

## Delivered files
| File | What it is |
|---|---|
| `longevity_labour_market.ipynb` | The complete, self-contained Colab notebook: installs libraries, downloads data, builds the person-year engine and the 5-model ensemble, forecasts supply/demand/balance to 2033, validates by backtest, and renders all charts and conclusions. |
| `readme.md` | This file — the case, our method, the results, how to run, data sources, requirements, and the file manifest. |
| `requirements.txt` | The Python libraries (with versions) the notebook needs. |
| `authors.md` | The list of authors (team Primus). |

## Full project
Extended analysis, methodology, an interactive bilingual site, slide decks and a
narrated video: **https://github.com/rossikeh-ops/longevity-labour-market**

## License
MIT
