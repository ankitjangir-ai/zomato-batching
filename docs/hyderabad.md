# Hyderabad (Tier 1)

## Why this city
A large Tier 1 metro, used to test whether results hold in a much bigger and denser market.

## Setup
Built with the same method as Hubli-Dharwad, so results are directly comparable.
Notebooks: `notebooks/hyderabad/`
Data: `data/hyderabad/`

## Greedy baseline
From `results/hyderabad/baseline/baseline_metrics.json` (16,856 orders):
- Partners used: 996
- Total distance: 86,196.76 km
- Average delivery distance: 2.79 km
- Missed batch count: 924 (5.48% of orders)
- Estimated daily cost: Rs 279,466.99

## Batching scenarios
Same two eligibility rules as Hubli-Dharwad:
- **Q (headline):** orders within a 1.5 km proximity threshold taken from the literature. This is the conservative case.
- **P (sensitivity):** orders in the same zone only, an assumption made for this project. This is the aggressive case.
- **Avg:** the mean of P and Q, used as the primary figure in the financial and national models.

## Batching result
Change vs greedy baseline:

| Metric | Q (conservative) | Avg (primary) | P (aggressive) |
|--------|------------------|---------------|----------------|
| Partners used | 996 to 961 (-3.5%) | 996 to 926 (-7.0%) | 996 to 891 (-10.5%) |
| Total distance | -1.1% | -1.0% | -0.9% |
| Missed batch count | 924 to 172 (-81.4%) | 924 to 173 (-81.3%) | 924 to 174 (-81.2%) |
| Estimated daily cost | Rs 275,532.55 (-1.4%) | Rs 274,368 (-1.8%) | Rs 273,203.57 (-2.2%) |

## Financial estimate
Simulated annual cost saving for the city (daily saving x 365):

| Q (conservative) | Avg (primary) | P (aggressive) |
|------------------|---------------|----------------|
| Rs 0.1436 crore | **Rs 0.1861 crore** | Rs 0.2286 crore |

The primary estimate of Rs 0.1861 crore is about Rs 18.6 lakh per year for the city.

## How it differs from Hubli-Dharwad
- Under Q, Hyderabad shows larger percentage cuts in partners (-3.5% vs -0.8%) and cost (-1.4% vs -1.2%); distance is similar (-1.1% vs -1.2%).
- Under Avg and P, Hubli-Dharwad shows larger percentage cuts in partners (-18.0% and -35.3% vs -7.0% and -10.5%).
- The absolute annual saving is larger in Hyderabad in every scenario (Avg: Rs 0.1861 crore vs Rs 0.0461 crore), because the city has far more orders (16,856 vs 1,515).

## Figures
`figures/hyderabad/`: baseline, batching, greedy_vs_smart, financial
