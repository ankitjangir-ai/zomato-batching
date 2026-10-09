# Methodology

These are the modelling decisions that were fixed during the project, and the reasons for them.

## Data anchoring
All parameters come from published sources instead of assumptions: Eternal (Zomato) annual reports for FY24 to FY26, CDP Scope 3 emissions disclosures, and Census figures. Three-year averages are used consistently.

Other sources: Goodreturns (petrol prices) and FSSAI guidelines.

## City model
- **Supply-side weight:** 0.60
- **Demand-side weight:** 0.80, with a 1.18 student uplift
- **GOV/NOV discount rate:** 14.85%, derived from the reports
- The student uplift applies to **demand only** (orders and restaurants). It is not applied to delivery partners or delivery distance, to avoid double-counting.

## Batching rules
- Two orders can be batched only if their destinations are within **0.5 km** of each other. This is checked before any batching is allowed.
- Synthetic destinations are generated as **20% at the exact same centroid** and **80% within 0 to 0.5 km** of it at random.
- Partner capacity is modelled as hourly shift targets, not as individual partners.

## Distance measurement
Two distances are kept separate so pickup kilometres are never counted twice:
- `avg_delivery_distance_km`: restaurant to customer only
- `avg_total_trip_distance_km`: the full trip, comparable to CDP figures

Zone-level distances are held in a matrix in seconds, and distance within a zone uses a geometric formula.

## Cost model
Two components: a fixed per-delivery incentive plus a variable fuel cost per kilometre. The national average petrol price (Rs 111.21/L) is used for both cities so they can be compared like for like, even though it is less accurate locally.

## Tools
OR-Tools (CVRP), XGBoost (classifier), OSMnx (road network, projected to EPSG:32643), Python on Google Colab and Jupyter.

## Principles
- **Partner utilisation, not headcount.** The goal is the same partners travelling fewer kilometres. Results are described as improved utilisation, not "partners saved".
- **Consistency over local accuracy** when comparing cities.
- **Focus on the core contribution.** Peripheral parameters were deliberately kept simple so they would not distract from the batching result.
