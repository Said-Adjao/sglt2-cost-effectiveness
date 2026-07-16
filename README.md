# Cost-Effectiveness of SGLT2 Inhibitors for Heart Failure Prevention in Type 2 Diabetes with Established ASCVD

A reproducible Markov cost-effectiveness model with deterministic and probabilistic sensitivity analysis, built in R and reported with Quarto. The treatment-effect input comes from an independent meta-analysis (see companion repository).

## Summary

This analysis estimates the cost-effectiveness of SGLT2 inhibitors versus placebo for preventing heart failure hospitalization in adults with type 2 diabetes and established atherosclerotic cardiovascular disease (ASCVD). A three-state Markov model (Stable → Post-HF hospitalization → Dead) was run over a 20-year horizon with 3% discounting.

**Key finding:** at list price (\$6,000/year), the base-case ICER was **~\$276,000 per QALY** — above the US willingness-to-pay threshold. The conclusion was **robust to uncertainty in the treatment effect** (HR 0.62–0.78) but **highly sensitive to drug price**: SGLT2i reaches the \$150,000/QALY threshold at an annual price of ~\$3,300. Probabilistic sensitivity analysis (5,000 simulations) found a ~6% probability of cost-effectiveness at \$150,000/QALY at list price.

This demonstrates a core HEOR principle: **clinical effectiveness does not guarantee cost-effectiveness.** A drug with a strong relative effect (30% reduction in HF hospitalization) can still represent poor value at list price, depending on absolute event rates and cost.

## Methods

- **Model:** three-state Markov (state-transition) model, 20 annual cycles, 3% discounting of costs and QALYs
- **Treatment effect:** HR 0.70 (95% CI 0.62–0.78) for HF hospitalization, from an independent meta-analysis of 4 cardiovascular outcome trials
- **Deterministic sensitivity analysis:** one-way on treatment effect (across its 95% CI) and on drug price (threshold analysis)
- **Probabilistic sensitivity analysis:** 5,000 Monte Carlo simulations with Beta (probabilities, utilities), Gamma (costs), and log-normal (hazard ratio) distributions; cost-effectiveness plane and acceptability curve (CEAC)
- **Cross-validation:** the base-case model was independently rebuilt in `heemod`, an established R package for health economic modeling. Reconciling the two implementations required accounting for differences in half-cycle correction and discount-timing conventions — both approaches converged on the same substantive conclusion.
- **Reporting:** fully reproducible Quarto document — every figure and statistic, including the PSA, regenerates from code

## Files

- `sglt2_cea_report.qmd` — Quarto source (the full reproducible analysis)
- `sglt2_cea_report.html` — rendered report
- `cost_effectiveness_cheat_sheet.md` — a general reference for building cost-effectiveness models in R

## Limitations

Simplified three-state structure with illustrative inputs (a definitive analysis would source and cite each parameter); list-price assumptions differ from negotiated net prices; recurrent-event costs simplified. Results demonstrate method rather than a definitive coverage recommendation.

## Companion work

The treatment-effect input was synthesized in a separate meta-analysis: [SGLT2i vs placebo meta-analysis](https://github.com/said-adjao/sglt2-hf-meta-analysis). Together these form an evidence-to-economics workflow.
sglt2_budget_impact_analysis

## Tools

R · `tidyverse` · `ggplot2` · Quarto · Markov modeling · Monte Carlo PSA

---
*Author: Said Adjao. Illustrative analysis built for demonstration; all data from published sources.*
