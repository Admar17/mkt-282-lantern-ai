# Lantern AI — MKT 282 capstone

Pricing, targeting, and lineup analysis for **Lantern AI**, a fictional privacy-first assistant (400,000 MAU, $0 revenue, paid launch 11 Jan 2027). Work lives in four Jupyter notebooks that follow the course milestones.

**Recommendation (Week 5).** One paid tier: **Lantern Pro at $24/month** — Standard usage, Vault, life-admin with click-to-approve, full integrations, individual. 24-month NPV **$1.36 million**. Do not buy the GPU rider. No student plan.

Keep this repository **private**. The case PDF, Fact Pack, and practice CBC are course materials, not public data.

## What’s in here

| File | Milestone | What it answers |
|---|---|---|
| [`week2_target_and_size.ipynb`](week2_target_and_size.ipynb) | Target and size | Who inside 400k MAU should see the $15 launch credit |
| [`week3_instrument.ipynb`](week3_instrument.ipynb) | Instrument | MaxDiff grid, CBC spec, silicon-twin personas, preregistration |
| [`week4_measure.ipynb`](week4_measure.ipynb) | Measure | QA, importances, WTP, Exhibit 10, hypothesis verdicts |
| [`week5_decide.ipynb`](week5_decide.ipynb) | Decide | Lineup, NPV, capacity, refreshed \(p^*\), experiment |

This repo ships the notebooks and working data (Excel / CSV). PDFs are omitted.

```
Capstone/
├── README.md
├── requirements.txt
├── week2_target_and_size.ipynb
├── week3_instrument.ipynb
├── week4_measure.ipynb
├── week5_decide.ipynb
├── Week2/                             # memo + Excel supplement
└── Data/
    ├── Lantern_Fact_Pack.xlsx          # tabs 1–8; Week 2 uses 3–5
    ├── Lantern_Practice_CBC_Data.xlsx  # Week 4–5 until Discover HB lands
    ├── maxdiff_responses.csv
    ├── cbc_pilot_log.csv
    └── silicon_twin_personas.csv
```

Run every notebook from this folder so `Data/...` paths resolve.

## Headline results

**Week 2 — targeting.** Logit of `upgrade_intent_click` on pre-banner telemetry (n = 5,000). Honest holdout AUC **0.760**. Excluded `plans_page_views_24h_post_banner` (post-banner leakage). Planning numbers from Fact Pack tab 4: \(V = \$24.70\), \(c = \$3.40\), \(p^* = c/V = 13.8\%\). **102,320** of 400,000 clear the cutoff. Targeted EV **+$190k** vs **−$388k** show-everyone.

**Week 3 — instrument.** Working grid is Exhibit 8 (usage, privacy, agents, integrations, household, price $6–$36). 12 MaxDiff tasks, dual-response none, 30 silicon personas (occupation mix 17 / 6 / 7). Preregistration cell is still **unsealed**.

**Week 4 — measure (practice CBC).** RLH < 0.45 drops 9 → **n = 391**. Price is 41.9% of importance. Median WTP: life-admin vs answers **$7.37**; no-training **$4.00**; Vault vs standard **$6.39**; household **$2.32**. $20 clone take **1.02%**. H2 confirmed; H3 killed; H1 complicated.

**Week 5 — decide.** First-choice × 124k qualified pool → Bass \(m\). Pro $24 take **16.1%**, NPV **$1.36M**. Clone $20 NPV **−$1.79M**. GPU rider: do not buy; trigger **15,500** seats. Refreshed \(V = \text{CLV} \times \text{take} = \$35.62\), \(p^* = 9.5\%\), **163,200** shown.

Weeks 4–5 currently score the **practice** CBC. When Discover HB arrives, point `UTILITIES_PATH` at that file and re-run.

## Setup

```bash
python3 -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

Needs Python 3.11+ (developed on 3.13). No API keys. The only inputs are the files under `Data/`.

## Notes for reviewers

- **V and c are not estimated.** They are Lantern finance planning numbers on Fact Pack tab 4. Week 2 only computes \(p^* = c/V\). Week 5 replaces planning \(V\) with CLV × take.
- **Do not use** `plans_page_views_24h_post_banner` as a predictor. Click rate is 0% when views = 0; every clicker has at least one view.
- The conjoint sample stands in for the **124,000** consideration set (pulse: very/somewhat likely to pay), not all 400,000 MAU.
- Official `Lantern_Lineup_Simulator_Template.xlsx` is not in this folder. Week 5 implements the engine from Fact Pack tabs 1, 6, 7, and 8.
