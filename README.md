# A/B Testing: E‑commerce Landing Page Experiment

Analyze results of an A/B test (old vs. new landing page) for an e-commerce website using hypothesis testing and regression.

## Dataset
- `ab_data.csv`: user_id, timestamp, group (control/treatment), landing_page (old/new), converted (0/1)
- `countries.csv`: user_id, country (US/UK/CA)  
Source: Kaggle (A/B testing dataset)

## What’s in this project
- **Data cleaning**
  - Remove rows where `group` and `landing_page` don’t align
  - Remove duplicate user observation
- **Part 1: Descriptive conversion rates**
  - Overall conversion rate
  - Conversion rate by control vs. treatment
- **Part 2: A/B hypothesis test**
  - Simulation-based approach to estimate p-value
  - Built-in **two-proportion z-test** via `statsmodels`
- **Part 3: Logistic regression**
  - `converted ~ ab_page` (treatment indicator)
  - Add **country** controls: `converted ~ ab_page + CA + UK` (US baseline)
- **Part 4: Day-of-week analysis**
  - Create day-of-week features from timestamp
  - Logistic regression using day dummies
  - Focused comparison between **Monday vs Friday**
- **Part 5: Should the test run longer?**
  - Aggregate daily conversion rates for old/new pages
  - Linear regression of daily rates vs. time (date encoded numerically)

## Key findings (summary)
- **New page does not outperform old page**: both hypothesis testing and logistic regression fail to show a statistically significant lift for the new page.
- **Country** does not show strong evidence of affecting conversion in this dataset.
- **Day-of-week effects** are generally weak; a focused Monday vs Friday comparison may show a small difference, but overall evidence is limited.
- **No meaningful time trend** in conversion rates over the experiment window; extending the test is unlikely to change conclusions.

## How to run
1. Open `notebook.ipynb` in VS Code (Jupyter).
2. Ensure the following packages are installed:
   - `pandas`, `numpy`, `matplotlib`, `statsmodels`, `scipy`
3. Run cells top-to-bottom.

## Project files
- `notebook.ipynb` — full analysis (cleaning, tests, regressions, visuals)
- `ab_data.csv` — experiment data
- `countries.csv` — country mapping