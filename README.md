# Performance Analytics Framework 

<img src="https://placehold.jp/24/1F5FA6/1F5FA6/1500x10.png?text=%20" width="100%" height="3px" />

**Goal**  
Create a reusable performance analysis engine that allows leaders to diagnose *why* results are good or bad, not just *what* happened, without leaving the dashboard.

**Outcomes**
- Built an interdependent calculation group framework that scales a single performance dashboard across multiple metrics and comparison modes.
- Enabled baseline vs comparison analysis across budget, goal, and time, with both raw and percent variance.
- Implemented selectable time comparisons (MTD, YTD, trailing periods, and prior week/month/year) to support fast root-cause diagnosis.

**Approach**  
Designed a stack of calculation groups that separate three concerns, metric selection, comparison logic, and time framing, while maintaining stable behavior under different filter contexts (location, provider, date). The framework abstracts analysis patterns so the same dashboard design can be reused across multiple KPIs without duplicating measures.

**Tools**  
Power BI (Modeling & Visualization) · DAX · Calculation Groups (Tabular Editor) · SSAS / Semantic Model

<img src="https://placehold.jp/24/1F5FA6/1F5FA6/1500x10.png?text=%20" width="100%" height="3px" />

# Framework Capabilities
- Metric-agnostic performance views (scale one dashboard across multiple KPIs)
- Baseline vs comparison (Budget, Goal, Time) with variance and variance %
- Selectable time comparisons (MTD, YTD, Trailing 3/6 Months, Previous Month, Previous Year, Previous Week)
- Consistent filter behavior across location, provider, and date contexts

<img src="https://placehold.jp/24/1F5FA6/1F5FA6/1500x10.png?text=%20" width="100%" height="3px" />

# Projects
- Calculation Group Architecture
- Comparison Modes (Budget, Goal, Time)
- Time Comparison Selector
- Implementation Notes and Tradeoffs

<img src="https://placehold.jp/24/1F5FA6/1F5FA6/1500x10.png?text=%20" width="100%" height="3px" />

## 1) Calculation Group Architecture

![Framework Architecture Diagram](/calculation_group_schema.png)

Stacked calculation groups designed to parameterize performance analysis along three dimensions: metric, comparison mode, and time framing.

**Focus Areas**
- Separation of concerns (metric selection vs comparison vs time intelligence)
- Interdependent ordering to avoid filter-context conflicts
- Reusability across KPIs without measure duplication
- Stable behavior under slicers (practice, provider, month, day)

<img src="https://placehold.jp/24/1F5FA6/1F5FA6/1500x10.png?text=%20" width="100%" height="3px" />

## 2) Comparison Modes (Budget, Goal, Time)

![Comparison Modes](/variance_dashboard.png)

A standardized approach to comparing baseline performance against different benchmarks, with both raw and percent variance.

**Focus Areas**
- Baseline vs Budget
- Baseline vs Goal
- Baseline vs Time (prior period comparison)
- Variance and variance % applied consistently across metrics

<img src="https://placehold.jp/24/1F5FA6/1F5FA6/1500x10.png?text=%20" width="100%" height="3px" />

## 3) Time Comparison Selector

![Time Comparison Selector](/time_series_selector.png)

Time intelligence selector enabling managers to shift the comparison window without changing measures or rebuilding visuals.

**Focus Areas**
- MTD and YTD comparisons
- Trailing 3 and trailing 6 month comparisons
- Previous month and previous year comparisons
- Previous week comparisons
- Guardrails to prevent “flattened” visuals due to incorrect scoping

<img src="https://placehold.jp/24/1F5FA6/1F5FA6/1500x10.png?text=%20" width="100%" height="3px" />

## 4) Implementation Notes and Tradeoffs

**Tradeoffs**
- Normalization is non-trivial when a dashboard mixes normalized and non-normalized visuals under shared selectors. A clean normalization layer likely requires either (1) a parallel normalized metric layer, or (2) a redesigned visual contract where normalization is consistently applied across all visuals on a page.

**Next Iteration**
- Introduce a dedicated normalization layer (per doctor day, per visit, per business day) that remains compatible with the calculation group stack.
- Expand guardrails for edge cases where dates with data differ across metrics or locations.
