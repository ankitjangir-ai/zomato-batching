# National Models

The two city results are combined to estimate effects at national scale.

## Inputs
- Financial and distance results from both cities
- Eternal annual report figures for platform scale
- CDP Scope 3 emissions disclosures
- National average petrol price: Rs 111.21/L

## Financial model
The model scales each city saving to national level in four steps. (1) Per-order saving: each city daily cost saving is divided by its simulated daily orders (1,515 for Hubli-Dharwad, 16,856 for Hyderabad), separately for Q, Avg and P. (2) Blending: the two per-order savings are combined as a weighted average by simulated order share, about 8% Hubli-Dharwad and 92% Hyderabad. (3) Scaling: the blended per-order saving is multiplied by national daily orders, which is the notebook average annual order figure divided by 365. (4) Annualising: the daily national saving is multiplied by 365. Avg is the primary scenario, with Q and P as the range. Assumptions: the two simulated cities are treated as representative of all of India, the weighting follows simulated order counts rather than real city shares, and the per-order saving is the same at every order volume.
Notebook: `notebooks/national/financial_model.ipynb`
Figures: `figures/national/financial/`

## Environmental model
Estimated emissions reduction at national scale: about **2,580 tonnes CO2e per year** (primary Avg(P,Q) scenario, range 2,248 to 2,912 tonnes; see `results/national/environmental_metrics.json`).
Notebook: `notebooks/national/environmental_impact.ipynb`
Figures: `figures/national/environmental/`

## Reading these numbers
These are projections. They extend results from two simulated cities to a whole country, so they carry the assumptions of both cities and of the scaling step. They show the order of magnitude, not a forecast.
