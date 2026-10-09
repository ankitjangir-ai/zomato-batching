# Project Flow

The project runs in five phases. Each phase feeds the next, and the same method is applied to both cities.

1. **Build City Network.** Create a synthetic city (zones, road network, restaurants, order demand) anchored to official data.
   Notebooks: `01_build_city_network` (Hubli-Dharwad), `01_build_city` (Hyderabad)
   Outputs: `city.csv`, `districts.csv`, `orders.csv`, `restaurants.csv`, `simulation_config.json`, `zone_distance_matrix.npy`

2. **Greedy Baseline.** Dispatch orders the way the current system appears to behave: one order per partner, assigned greedily.
   Notebook: `02_greedy_baseline`
   Outputs: `baseline_metrics.json`, `greedy_dispatch_log.csv`, `baseline_summary.png`

3. **Batching Optimized Dispatch.** Group eligible orders using OR-Tools capacitated vehicle routing (CVRP), with an XGBoost classifier supporting batch decisions.
   Notebook: `03_batching`
   Outputs: smart dispatch logs and metrics, `cvrp_assignments.csv`, `classifier.pkl`, comparison figures

4. **Financial Model.** Convert distance and partner savings into annual cost savings per city, with a primary estimate, a range, and two sub-models (P and Q).
   Outputs: figures in `figures/<city>/financial/`

5. **Environmental Impact and National Scale.** Extend city results to national estimates of cost and emissions.
   Notebooks: `national/financial_model`, `national/environmental_impact`

Each city is run through phases 1 to 4 separately. Phase 5 combines both.
