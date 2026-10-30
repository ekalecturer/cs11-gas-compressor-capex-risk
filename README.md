# Gas Compressor Capex, PLTG 4x25 MW Maleo-Gorontalo: Where Does a US$7.1M Decision Break?

**Case Study #11 in *The Feasibility Stress Test*. Primary lens: Capex Planning.**

An open-source Python reconstruction and browser simulator of a published Indonesian investment evaluation: a gas compressor for a 4 x 25 MW gas-turbine plant, built-operated-owned by a subsidiary of PT Pelayanan Listrik Nasional Batam. The base case clears at a thin margin. This repo shows which inputs the margin depends on.

## The case

Gas compressor for PLTG 4 x 25 MW Maleo-Gorontalo. Investor PT XYZ (BOO scheme), project owner PT PLN Gas Geothermal. Capex US$7,118,174 including 10% VAT (PPN). Contract life 24 months under a Letter of Intent, with an option to extend to 5 years (not modelled in the paper). WACC 9% at 70:30 debt-to-equity.

## Citation

Siregar, A. & Wiryono, S. (2021). *Implementation Monte Carlo Simulation in Investment Evaluation: Case Study - Gas Compressor Investment PLTG 4 x 25 MW Maleo-Gorontalo.* Proceedings of the 3rd International Conference on Applied Economics and Social Science (ICAESS 2021), pp. 72-79. SCITEPRESS. https://doi.org/10.5220/0010935100003255

## Confirmed findings (paper's own tables)

| Metric | Value |
|---|---|
| Capex | US$7,118,174 |
| Base NPV (WACC 9%) | US$500,444 (7.0% of capex, own arithmetic) |
| IRR / PI / payback | 11.50% / 1.08 / 1.57 years |
| Capex +10% | NPV US$32,019 (-93.6%) |
| Capex -10% | NPV US$968,869 |
| Life 18 / 30 months | NPV US$93,955 / US$879,563 |
| D:E 80:20 / 60:40 | NPV US$655,908 / US$350,429 |
| Monte Carlo (1,000 iterations) | mean US$474,346, SD US$375,429, P(NPV<0) 10.32% |

Recommendation in the paper: proceed. The paper reports no post-decision outcome; it is a prospective study.

## Reconstruction results (ILLUSTRATIVE, not the authors' numbers)

| Statistic | Paper | Reconstruction (20,000 trials) |
|---|---|---|
| Mean NPV | 474,346 | 497,784 |
| SD | 375,429 | 359,731 |
| P(NPV<0) | 10.32% | 9.3% |

Own arithmetic: break-even capex overrun about +10.7% (US$760,474, linear read of Table 7). Share of explained variance: capex 58%, contract life 39%, debt mix 3%. Hypothetical levers in the model: fixed-price capex cuts P(NPV<0) from 9.3% to 0.2%; guaranteed 24-month life cuts it to 1.1%.

## Honesty disclosure

- **Full text was read through automated extraction** of the SCITEPRESS page, not a manual PDF review. Check numbers against the paper before reuse.
- The paper does **not** publish its cash flows, tariff, tax rate, depreciation, numeric Monte Carlo bounds, or the triangular mode. This is **not** a cash-flow rebuild. It is a response surface: base NPV plus three effects, each interpolated through the paper's Table 7. It reproduces those six points by construction.
- Monte Carlo bounds (capex +/-10%, life 18-30 months, debt share 60-80% with mode 70%) are **my assumption**, taken from the sensitivity ranges. Additivity (no interaction) is also assumed.
- The paper has internal inconsistencies (for example best-case payback longer than base case; Figure 9 labelled normal while Table 9 says triangular). The reconstruction does not attempt payback or IRR.
- Capex bias scenarios above +10% extrapolate the sensitivity line beyond the paper's range.

## Run it

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute notebook.ipynb
```

Or open `docs/index.html` in a browser for the interactive simulator (no build step). Enable GitHub Pages on the `docs/` folder to host it.

## License

MIT, copyright 2026 Eka Krisna Santoso. See `LICENSE`. The source paper remains the authors' work.

---
Part of **The Feasibility Stress Test**: real Monte Carlo and financial-engineering case studies for capex decisions.
