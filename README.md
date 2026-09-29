# 🍩 Strategic Operations & Quantitative Forecasting: "Donuts to Go" Decision Model

An interconnected, 4-phase quantitative business model built in Microsoft Excel to evaluate market demand, simulate production capacity constraints, and guide strategic capital expansion (Current Operations vs. Franchise Expansion vs. Mobile Food Truck Launch) under conditions of risk and uncertainty.

---

## 📖 Executive Summary & Business Scenario

### The Strategic Dilemma
"Donuts to Go" is an established operating business facing critical growth decisions. Leadership needed to determine how to scale:
* **Option 1: Current Operations** — Maintain existing brick-and-mortar capacity (4,000 units/month).
* **Option 2: Franchise Expansion** — Scale production capacity to 5,280 units/month with higher overhead.
* **Option 3: Mobile Food Truck** — Pivot into a flexible make-to-order operation targeting varying venue types (offices vs. weekend events).

Each operational path carried distinct trade-offs:
* **Underproduction:** Leads to stockout penalties ($3.00/unit lost customer goodwill) and missed revenue.
* **Overproduction:** Leads to excess inventory and forced discounted salvage sales ($1.25/unit).
* **Location Volatility:** Mobile demand fluctuates significantly depending on operational hours and location profiles.

### The Sequential 4-Stage Architecture
This project was constructed as a strictly dependent, 4-stage analytical pipeline across 8 worksheets. A calculation error or misaligned cell coordinate in Phase 1 or 2 would automatically corrupt downstream monthly P&Ls in Phase 3 and distort final decision payoff tables in Phase 4. Executing this required rigorous formula auditing, strict data validation, and clean reference structuring.

---

## 🔍 The 4-Phase Analytical Breakdown
[Phase 1: Baseline Demand & Unit Economics]
│
▼
[Phase 2: Time-Series Decomposition & Linear Regression]
│
▼
[Phase 3: Capacity Constraints & Inventory Economics]
│
▼
[Phase 4: Multiple Regression & Decision Theory Analysis]

### Phase 1: Baseline Demand Auditing & Unit Economics
* **Exploratory Data Analysis:** Cleaned historical transaction records (2020–2022) using Excel Pivot Tables and dynamic Pivot Charts to isolate monthly demand distributions.
* **Unit Economics Modeling:** Structured baseline revenue and variable cost schedules assuming standard customer bundling (1 coffee at $2.99 + 1 donut at $2.50).
* **Cost Segmentation:** Classified fixed operating overhead (insurance, equipment maintenance, facilities) versus unit variable costs (ingredients, cups, paper products).

### Phase 2: Time-Series Decomposition & Linear Regression
* **Seasonal Index (SI) Calculation:** Quantified cyclical swings by isolating monthly demand against annual baselines to derive a 3-year average seasonal factor for every calendar month.
* **Deseasonalization:** Normalized historical figures by stripping out seasonality to identify the underlying growth trajectory:
  $$\text{Deseasonalized Demand} = \frac{\text{Actual Demand}}{\text{Seasonal Index}}$$
* **Linear Trendline Modeling:** Executed simple linear regression ($Y = mx + b$) on 36 months of deseasonalized demand ($t = 1 \dots 36$) using the Data Analysis Toolpak to project baseline demand for future fiscal cycles.

### Phase 3: Capacity Constraints & Inventory Financials
Simulated a full 12-month operating calendar for **Current Operations** (capped at 4,000 units/mo) versus **Franchise Operations** (capped at 5,280 units/mo) across Low, Average, and High demand states:
* **Capacity Logic:** Built dynamic formulas to separate demand into satisfied sales versus constrained shortfalls:
  $$\text{Satisfied Demand} = \min(\text{Monthly Demand}, \text{Monthly Capacity})$$
* **Surplus Salvage Recovery:** Evaluated monthly inventory surplus and modeled secondary revenue recovery through day-old discounted sales ($1.25/unit).
* **Stockout Penalties:** Accounted for unmet demand penalties ($3.00/unit) to reflect lost customer goodwill and churn risk.
* **Dynamic Monthly P&Ls:** Structured complete annual financial schedules calculating gross revenue, ingredient expenses, salvage income, stockout losses, and annual net profit.

### Phase 4: Multiple Regression & Decision Theory Under Uncertainty
* **Predictive Multiple Regression:** Modeled mobile Food Truck demand using historical operating hours and location categorical variables (Event Location vs. Office Location) via binary dummy variable encoding ($1, 0$).
* **Make-to-Order Structure:** Modeled Food Truck economics under a flexible workflow (zero inventory overage, zero stockout penalties, adaptable variable labor hours).
* **Payoff Matrix Synthesis:** Aggregated annual net profits across all three strategic alternatives under three states of nature:

| Strategic Alternative | Low Demand State | Average Demand State | High Demand State |
| :--- | :---: | :---: | :---: |
| **Current Operations** | **$86,688.55** | $111,605.66 | $99,900.02 |
| **Franchise Operations** | $72,488.04 | **$114,133.09** | $109,681.03 |
| **Food Truck Expansion**| $60,155.66 | $109,752.02 | **$110,717.36** |

* **Decision Analysis Under Ignorance (Non-Probabilistic):**
  * **Maximin (Pessimistic / Risk-Averse):** Recommends **Current Operations** ($86,688.55) to guarantee the highest worst-case profit floor.
  * **Maximax (Optimistic / Growth-Oriented):** Recommends **Franchise Operations** ($114,133.09) to capture peak upside potential.
  * **Laplace (Equal Likelihood):** Favors **Current Operations** ($99,398.08 average payoff).
  * **Minimax Regret:** Identifies **Current Operations** as the optimal choice to minimize maximum potential regret ($10,817.34).
* **Probabilistic Risk Analysis:**
  * **Expected Value Under Imperfect Information (EVUII):** Evaluated probability-weighted returns across states of nature.
  * **Expected Opportunity Loss (EOL):** Confirmed that **Franchise Operations** carried the lowest overall risk penalty ($3,099.19), proving it mathematically superior if market demand probabilities remain stable.

---

## 🛠️ Excel Functions & Technical Techniques Used

* **Regression & Statistical Modeling:** Data Analysis Toolpak (Single & Multiple Linear Regression, $R^2$, Adjusted $R^2$, ANOVA, P-values, coefficients).
* **Logical Conditionals:** Enforced capacity thresholds, salvage recovery, and inventory stockouts using nested `IF`, `MIN`, and `MAX` functions:
  * Overage: `=IF(Production > Demand, Production - Demand, 0)`
  * Shortage: `=IF(Demand > Production, Demand - Production, 0)`
* **Data Linking & Hygiene:** Connected 8 distinct sheets without circular references or `#REF!` errors, using strict cell formatting, coordinate referencing, and formula auditing.

---

## 🤝 Peer Mentorship & Collaboration

Because this project was structured as a 4-part sequential pipeline where any mistake in early phases broke all downstream numbers, formula troubleshooting was common across the cohort:
* **Logic Auditing & Debugging:** Guided classmates through tracing precedents and dependents in their workbooks to locate where cell references diverged.
* **Demystifying Quantitative Methods:** Translated technical concepts—such as dummy variable encoding, seasonal index isolation, and Minimax Regret matrices—into clear, step-by-step logic.
* **Supportive Problem Solving:** Fostered a "let's figure it out together" environment where peers felt comfortable asking questions and gaining confidence in their quantitative skills.
