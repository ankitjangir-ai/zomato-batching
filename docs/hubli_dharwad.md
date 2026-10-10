# Hubli-Dharwad (Tier 2)

## Why this city
It is a Tier 2 city and the author's home region, and it provides the smaller-city counterpart to Hyderabad.

## Setup
Synthetic city built from official data (see [methodology.md](methodology.md)) with a road network from OSMnx.
Notebooks: `notebooks/hubli_dharwad/`
Data: `data/hubli_dharwad/`

## Greedy baseline
From `results/hubli_dharwad/baseline/baseline_metrics.json` (1,515 orders, all dispatched):
- Partners used: 133
- Total distance: 11,882.28 km
- Average delivery distance: 4.33 km
- Missed batch count: 25 (1.65% of orders)
- Estimated daily cost: Rs 38,352.74

## Batching scenarios
Two eligibility rules are tested:
- **Q (headline):** orders within a 1.5 km proximity threshold taken from the literature. This is the conservative case.
- **P (sensitivity):** orders in the same zone only, an assumption made for this project. This is the aggressive case.
- **Avg:** the mean of P and Q, used as the primary figure in the financial and national models.

## Batching result
Change vs greedy baseline:

| Metric | Q (conservative) | Avg (primary) | P (aggressive) |
|--------|------------------|---------------|----------------|
| Partners used | 133 to 132 (-0.8%) | 133 to 109 (-18.0%) | 133 to 86 (-35.3%) |
| Total distance | -1.2% | -0.9% | -0.6% |
| Missed batch count | 25 to 16 (-36.0%) | 25 to 16 (-36.0%) | 25 to 16 (-36.0%) |
| Estimated daily cost | Rs 37,911.67 (-1.2%) | Rs 37,090.70 (-3.3%) | Rs 36,269.74 (-5.4%) |

## Financial estimate
Simulated annual cost saving for the city (daily saving x 365):

| Q (conservative) | Avg (primary) | P (aggressive) |
|------------------|---------------|----------------|
| Rs 0.0161 crore | **Rs 0.0461 crore** | Rs 0.0760 crore |

The primary estimate of Rs 0.0461 crore is about Rs 4.6 lakh per year for the city.

## Figures
`figures/hubli_dharwad/`: baseline, batching, greedy_vs_smart, financial
