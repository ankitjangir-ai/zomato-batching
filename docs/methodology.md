# Methodology

These are the modelling decisions that were fixed during the project, and the reasons for them.

## Data anchoring
Platform-scale inputs come from published sources: Eternal (Zomato) annual reports for FY24 to FY26, CDP Scope 3 emissions disclosures, and Census figures. Three-year averages are used consistently. Some modelling choices are the project's own assumptions rather than published figures, including the student demand uplift, the same-zone (P) batching rule, the generated destination shares, and the mileage used for fuel. These are listed where they are used and in [limitations.md](limitations.md).

Other sources: Goodreturns (petrol prices) and FSSAI guidelines.

## City model
- **Student demand uplift:** 1.18, an assumption made for this project. Final demand weights across each city's zones sum to 1.
- **GOV/NOV discount rate:** 14.85%, derived from the reports
- The student uplift applies to **demand only** (orders and restaurants). It is not applied to delivery partners or delivery distance, to avoid double-counting.

## Batching rules
Two eligibility rules are tested, and results are reported as a range:
- **Q (headline, conservative):** two orders can be batched only if their destinations are within **1.5 km**. This is a fixed threshold anchored to the "1 mile" proximity example in a food-delivery batching patent, rounded down.
- **P (sensitivity, aggressive):** two orders can be batched only if their destinations are in the **same zone**. This is an assumption made for this project.
- **Avg (primary):** the mean of the P and Q results, used in the financial and national models.
- Destinations are generated at zone level, not observed. In Hubli-Dharwad 75% of orders are delivered within the restaurant's own zone, and in Hyderabad 90%. In both cities, 90% of cross-zone orders go to nearby zones.
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
