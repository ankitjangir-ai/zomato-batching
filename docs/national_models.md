# National Models

The two city results are combined to estimate effects at national scale.

## Inputs
- Financial and distance results from both cities
- Eternal annual report figures for platform scale
- CDP Scope 3 emissions disclosures
- National average petrol price: Rs 111.21/L

## Financial model
[Describe how the city savings are scaled: per-order saving, then multiplied by national order volume. List the assumptions.]
Notebook: `notebooks/national/financial_model.ipynb`
Figures: `figures/national/financial/`

## Environmental model
Estimated emissions reduction at national scale: about **2,580 tonnes CO2e per year** (primary Avg(P,Q) scenario, range 2,248 to 2,912 tonnes; see `results/national/environmental_metrics.json`).
Notebook: `notebooks/national/environmental_impact.ipynb`
Figures: `figures/national/environmental/`

## Reading these numbers
These are projections. They extend results from two simulated cities to a whole country, so they carry the assumptions of both cities and of the scaling step. They show the order of magnitude, not a forecast.
