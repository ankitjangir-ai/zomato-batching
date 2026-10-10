# Key Findings

## Headline results

Q is the literature-anchored 1.5 km scenario (conservative), P is the same-zone-only scenario (aggressive), and Avg is the mean of the two.

| | Hubli-Dharwad (Tier 2) | Hyderabad (Tier 1) |
|---|---|---|
| Partners used (Q / Avg / P) | -0.8% / -18.0% / -35.3% | -3.5% / -7.0% / -10.5% |
| Total distance (Q / Avg / P) | -1.2% / -0.9% / -0.6% | -1.1% / -1.0% / -0.9% |
| Missed batch count (Q / Avg / P) | -36.0% / -36.0% / -36.0% | -81.4% / -81.3% / -81.2% |
| Estimated cost (Q / Avg / P) | -1.2% / -3.3% / -5.4% | -1.4% / -1.8% / -2.2% |
| Annual saving, Rs crore (Q / Avg / P) | 0.0161 / **0.0461** / 0.0760 | 0.1436 / **0.1861** / 0.2286 |

## What stands out
1. **Batching reduces missed batching opportunities in both cities.** The count falls by 36.0% in Hubli-Dharwad (25 to 16) and by about 81% in Hyderabad (924 to 172 under Q).
2. **The effect depends on the city and the scenario.** Under Q, Hyderabad shows slightly larger cuts in partners and cost, and distance savings are similar. Under Avg and P, Hubli-Dharwad shows larger cuts in partners. The simulation does not isolate why, so no cause is claimed here.
3. **Absolute savings are larger in the bigger city.** Hyderabad has 16,856 simulated orders against 1,515, and its annual saving is larger in every scenario.
4. **Distance savings are small everywhere.** They stay between about 0.6% and 1.2% in both cities.
5. **National projection:** about 2,580 tonnes CO2e per year (Avg of P and Q, range 2,248 to 2,912 tonnes between the two scenarios).

## Where to see the evidence
- Core comparison: `figures/<city>/batching/core_result_comparison.png`
- Greedy vs smart tables: `figures/<city>/greedy_vs_smart/`
- Financial figures: `figures/<city>/financial/`
- National figures: `figures/national/`

All results are simulated. See [limitations.md](limitations.md).
