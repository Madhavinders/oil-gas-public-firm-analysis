# Public Firm Analysis: US Oil & Gas Extraction (SIC 13)

Group project for BAIT 508 at UBC Sauder School of Business (MBAN), October 2026. It combines a quantitative analysis of 32 years of oil and gas firm data, a text analysis of 10-K business descriptions, and a peer benchmarking of EOG Resources that ends in one recommendation.

## Key findings

- **A churning sector.** 772 firms across 8,066 firm-years (1994-2025). Only 39 (5.1%) report in all 32 years.
- **Prices follow the oil cycle.** The average share price nearly halved in 2008 ($24.96 to $12.98) and bottomed at $12.46 in 2020.
- **Stable language, shifting edges.** Between 2020 and 2025, "drilling" falls from 45% to 35% of firms' top-10 TF-IDF keywords, while "reserves" (22% to 31%) and "emissions" (6% to 14%) gain share.
- **EOG earns more per dollar of assets than its peers.** It beat the peer-median ROA in 10 of 11 years (2015-2025), but its ROA fell from 18.8% in 2022 to 9.6% in 2025.
- **Recommendation.** Set an explicit return hurdle of about 13.5% ROA (EOG's own 2023-25 average) on acquisitions and major capital programs.

## Approach

**Part 1: Quantitative analysis.** Filter the Compustat-style panel to SIC major group 13, count firm-years and firms, and analyze stock prices, sales, geography, the 2008 crisis and return on assets.

**Part 2: Text analysis.** Clean the Item 1 text of 10-K filings, screen out filings that contain another company's text (159 to 119 firms in 2020), extract top-10 keywords with word counts and TF-IDF, train Word2Vec models, and compare 2020 with 2025 (119 vs. 85 firms).

**Part 3: Firm analysis and strategy.** Benchmark EOG Resources against nine US producers on revenue, market share and ROA (2015-2025), test whether asset growth was associated with higher returns, and recommend a return hurdle.

## Tech stack

Python, pandas, scikit-learn, NLTK, gensim, wordcloud, matplotlib

## Repository structure

```
oil-gas-public-firm-analysis/
├── README.md
├── requirements.txt
├── .gitignore
├── notebooks/
│   └── oil_gas_public_firm_analysis.ipynb
├── figures/          # exported charts
└── data/
    └── README.md     # how to obtain the course files (no raw data committed)
```

## Data

The datasets are course materials (public_firms.csv, major_groups.csv, 2020_10K_item1_full.csv, 2025_10K_item1_full.csv) and are not included in this repository. To reproduce the results, place the files in `data/`.

## How to run

```bash
pip install -r requirements.txt
python -c "import nltk; nltk.download('stopwords')"
jupyter notebook notebooks/oil_gas_public_firm_analysis.ipynb
```

## Limitations

- A 10-K labelled 2020 mostly describes fiscal 2019, so text and financial rows are matched by firm and the nearest fiscal year.
- About 1 in 4 oil and gas rows in the 2020 text file held another company's text. 40 filings were dropped after a name test and manual review. The 2025 file was screened more lightly.
- The peer group is small (10 firms) and the growth-ROA relationship is weak (r = -0.17), so the recommendation is a judgement supported by evidence, not a statistical proof.
- ROA uses year-end book assets and GAAP net income, so impairments and acquisition accounting can move it sharply.

## Team

- Anirudha Nair: Part 2, text analysis
- Karim Mazrou: Part 1, quantitative analysis, and report assembly
- Madhav Singh: Part 3, firm analysis and strategy

Generative AI tools were used as permitted by the course and are disclosed in the project report.
