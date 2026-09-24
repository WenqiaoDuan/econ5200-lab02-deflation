# econ5200-lab02-deflation
# Index Integrity — Deflation, Substitution Bias & Goodhart

## Objective

Develop and validate an index-integrity workflow that diagnoses deflation errors, quantifies substitution bias in consumer price measurement, and detects KPI distortion associated with Goodhart's Law.

## Methodology

* **Deflation pipeline diagnosis:** Audited the deflation workflow for unit, date-index, base-year, and alignment errors, identifying four distinct bugs, including an incorrect labeling of 1982–84 constant-dollar output as 2020 dollars.
* **Inflation-index comparison:** Compared annualized inflation measured by CPI-U and C-CPI-U to quantify the effect of upper-level substitution on measured price growth.
* **Bias interpretation:** Distinguished the annual inflation-rate differential from the cumulative index-level gap, avoiding an incorrect interpretation of the two metrics as equivalent measures of substitution bias.
* **KPI integrity analysis:** Examined the relationship between DAU/MAU and time per session across behavioral regimes and used correlation changes as a diagnostic signal for potential metric gaming.
* **Goodhart detection:** Identified a structural correlation reversal from strongly positive to strongly negative, treating the sign change as evidence of a changed incentive environment rather than as a causal estimate.
* **Productionization:** Packaged the corrected deflation logic in `deflation_utils.py` and validated `deflate_series()` with tests covering the identified failure modes.
* **Monitoring:** Built an interactive index-integrity monitor to visualize inflation measurement, cumulative index divergence, KPI relationships, and diagnostic signals.

## Key Findings

* The deflation audit identified **four pipeline bugs**, including a base-year labeling error that caused results expressed in **1982–84 dollars** to be incorrectly labeled as **2020 dollars**.
* Average annual inflation was **2.61% under CPI-U** versus **2.35% under C-CPI-U**, implying an **upper-level substitution differential of approximately 0.27 percentage points per year**.
* The **0.50 index-point annual cumulative gap** is a separate index-level measure and should **not** be interpreted as a 0.50 percentage-point substitution bias.
* The relationship between **DAU/MAU and time per session** shifted from **+0.93** in the organic phase to **−0.96** during the gaming phase. The correlation reversal provides a clear diagnostic signal of changing KPI incentives consistent with a Goodhart-type failure mode.
* The resulting workflow combines **data validation, index-number analysis, econometric diagnostics, automated testing, and interactive monitoring** into a reproducible index-integrity framework.
