# Hubli-Dharwad (Tier 2)

## Why this city
It is a Tier 2 city and the author's home region, and it provides the smaller-city counterpart to Hyderabad.

## Setup
Synthetic city built from official data (see [methodology.md](methodology.md)) with a road network from OSMnx.
Notebooks: `notebooks/hubli_dharwad/`
Data: `data/hubli_dharwad/`

## Greedy baseline
Reference metrics from the baseline run [confirm against `baseline_metrics.json`]:
- Overall unassigned rate: about 5%
- Average delivery distance: 8.11 km
- Missed batching rate: 6.94%

## Batching result
| Metric | Change vs greedy baseline |
|--------|---------------------------|
| Partners used | -31.6% |
| Total distance | -38.1% |
| Missed batch count | -97.4% |
| Estimated cost | -31.6% |

## Financial estimate
Primary estimate: **Rs 0.0461 crore per year** (about Rs 4.6 lakh) for the city.

## Figures
`figures/hubli_dharwad/`: baseline, batching, greedy_vs_smart, financial
