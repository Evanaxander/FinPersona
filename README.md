[README.md](https://github.com/user-attachments/files/33055737/README.md)
# FinPersona Bangladesh

### Who is left out of Bangladesh's financial system, and which lenders are at risk?

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR-GITHUB-USERNAME/finpersona-bangladesh/blob/main/FinPersona_Bangladesh.ipynb)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![scikit-learn](https://img.shields.io/badge/scikit--learn-LightGBM-orange)
![Data](https://img.shields.io/badge/data-World%20Bank%20%7C%20Dhaka%20Stock%20Exchange-green)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

A data-science study of Bangladesh's financial system. It looks at both sides of the market: the **people** who need financial services, and the **banks and NBFIs** that provide them. It uses only real, public data, and it runs free in Google Colab with no API keys or logins.

![Executive dashboard](figures/C1_executive_dashboard.png)

---

## Why this project

Every bank, NBFI and mobile-financial-services (MFS) company in Bangladesh faces two questions:

1. **Where is the untapped demand?** Who doesn't have an account yet, how many of them are there, and what's stopping them?
2. **Who is safe to work with?** Which lenders are healthy, and which are heading for trouble?

This project answers both with machine learning. It then checks its answers against a real event: the 2025 collapse and merger of five Bangladeshi banks.

---

## Key findings

### People: World Bank Global Findex 2025

| Finding | Number |
|---|---|
| Adults (15+) with an account | **43%**, down from 53% in 2021 |
| Adults with no account | **70 million** |
| Of those, own a mobile phone | **at least 48 million** |
| Gap vs. countries with similar phones, internet and digital skills | **−30 points** (−21 to −35 across 8 models) |
| "Missing" accounts implied by that gap | **about 36 million** |
| Largest gap | **Women: −41 points** |
| Adults who borrowed in the past year | **70%**, but only **12%** from a bank or NBFI |
| Adults who received a loan on their phone | **about 2%** |
| Main reason for having no bank/NBFI account | **Not enough money (82%)**, far ahead of distance or trust |

**In short:** Bangladesh has the phones but not the accounts. Demand for credit is huge but mostly informal. The fall since 2021 is about people **no longer using** accounts, so bringing them back may be cheaper than finding new customers.

### Institutions: Dhaka Stock Exchange, all listed banks and NBFIs

| Finding | Number |
|---|---|
| Early-warning model accuracy on banks and NBFIs it never saw (AUC) | **0.95** |
| Rank of the 5 banks later merged, using only prices up to 30 Sep 2025 | **#1 to #5 of 35** |
| Chance of that happening by luck | **1 in 324,632** |
| Listed NBFIs trading below face value (Tk 10) | **13 of 23** |
| Listed NBFIs with negative reserves | **61%** |

**The 2025 bank-merger test.** In November 2025, Bangladesh Bank merged First Security Islami, Global Islami, Social Islami, EXIM and Union Bank into Sammilito Islami Bank. In December 2025 it wrote their shares down to zero.

Before that, I rebuilt the early-warning model using **only share prices up to 30 September 2025**. It was trained on non-financial companies only, and it was given no information about the banks' balance sheets. It ranked exactly these five banks as the five riskiest of all 35 listed banks.

The market already had doubts about these banks, so the model didn't uncover anything secret. What it shows is that a simple, automatic screen would have put exactly these five banks at the top of a risk list before the regulator acted.

![Merger back-test](figures/B3_merger_backtest.png)

---

## What's inside the notebook

**Part A: People**
- Bangladesh trends from 2011 to 2024: accounts, mobile money, saving, borrowing and digital payments
- Gaps between groups: gender, income, education, work, age and location
- **Market sizing in millions of adults.** Findex gives only percentages, so the size of each group is worked out from the data itself, and the notebook checks this calculation.
- **Peer groups:** 92 low- and middle-income countries grouped by financial behaviour, to find the countries most like Bangladesh
- **Inclusion-gap model:** predicts the account ownership a country "should" have from its phone, internet and digital-skill levels. It is always tested on countries it has never seen, and it is run as 8 separate versions so the conclusions don't depend on one setup.

**Part B: Institutions**
- Health signals for every listed company: share returns, volatility, biggest drop, price compared with face value, trading activity, reserves and ownership
- **Lender types:** the 59 listed banks and NBFIs grouped into Sector Leaders, Weak Mid-tier, Distressed, and Distressed but speculatively traded
- **Early-warning model:** trained on non-financial companies and tested on banks and NBFIs
- **The 2025 bank-merger test**
- How IDLC, IPDC and the other NBFIs compare

**Part C: Executive dashboard**
- A one-page summary, uses for banks, NBFIs and MFS companies, and limitations

---

## Charts

| | |
|---|---|
| ![Trends](figures/A1_bangladesh_trends.png) | ![Gaps](figures/A2_inclusion_gaps.png) |
| ![Market sizing](figures/A3_market_sizing.png) | ![Reasons](figures/A4_reasons_and_coping.png) |
| ![Peer groups](figures/A5_peer_groups.png) | ![Inclusion gap](figures/A6_inclusion_gap.png) |
| ![Lender map](figures/B1_lender_map.png) | ![Distress scores](figures/B2_distress_scores.png) |

---

## How to run it

**In Google Colab (recommended, free):**
1. Click the **Open in Colab** badge at the top of this page.
2. Click **Runtime → Run all**.
3. Wait about 3–5 minutes. All data downloads automatically.

**On your own computer:**
```bash
git clone https://github.com/YOUR-GITHUB-USERNAME/finpersona-bangladesh.git
cd finpersona-bangladesh
pip install -r requirements.txt
jupyter notebook FinPersona_Bangladesh.ipynb
```

The DSE data is fixed at 5 October 2026, so your results match this page. To use the latest trading day instead, set `DSE_LIVE = True` in section 1 of the notebook.

---

## Data

| Source | What it contains | Access |
|---|---|---|
| [World Bank Global Findex 2025](https://www.worldbank.org/en/publication/globalfindex/download-data) | Nationally representative survey of adults in 140+ countries, 2011–2024, for all adults and 12 groups | Free, CC BY 4.0 |
| [Dhaka Stock Exchange](https://www.dsebd.org) via [dse-data](https://github.com/nifty1303/dse-data) | Daily prices for every listed company (Sep 2024 – Oct 2026), plus category (A/B/Z), shareholding, reserves and dividends | Free, public |

Before any analysis, the notebook checks the data against published World Bank figures: Bangladesh account ownership of 52.8% in 2021 and 43.3% in 2024. A copy of every source file is in `data/`.

**Why no individual customer data?** Bangladeshi banks don't publish customer records, because they're private. This project uses the best real public data instead of made-up data.

---

## Limitations

- **Findex data is by group, not by person.** It can't measure overlaps between groups (for example, poor *and* female), so some market sizes are minimums.
- **The inclusion-gap model explains about half of the differences between countries.** That's why the gap is shown as a range, and only conclusions shared by all 8 versions are stated.
- **Share-price history starts in September 2024.** A longer history would allow longer back-tests.
- **The Z category is a DSE rule about dividends and AGMs, not a credit rating.** The distress score is a screening tool, not investment advice.

---

## Repository layout

```
FinPersona_Bangladesh.ipynb   the full analysis, with all results saved
figures/                      every chart, ready to view
data/                         copies of the source files used for this report
requirements.txt              Python packages needed
LICENSE                       MIT
```

---

## About me

**Evan** — Dhaka, Bangladesh
[LinkedIn](https://www.linkedin.com/in/YOUR-LINKEDIN) · [Email](mailto:YOUR-EMAIL)

Questions, ideas or feedback are welcome: open an issue or get in touch.
