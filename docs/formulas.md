# Zomato Dispatch Simulation: Formulas and Assumptions

## Stage 1: Geography and Zones (`01_build_city`)

### F1 — Zone radius
**Formula:** `zone_radius = √(area_km² / π)`

**Meaning:** Treats each zone as a circle of equal area.

### F2 — Intra-zone distance
**Formula:** `intra_zone_dist = 0.9 × zone_radius`

**Meaning:** Average traversal inside a zone (matrix diagonal).

### F3 — Demand weights check
**Formula:** `Σ demand_weight = 1.0`

**Meaning:** Check on the 16 zone weights.

### F4 — Geodesic distance
**Formula:** `geodesic_km(z1, z2)` via `Geod.inv` on WGS84.

**Meaning:** Zone centroid-to-centroid distance.

---

## Stage 2: Supply Side

### F5 — Restaurant popularity weight
**Formula:** `popularity_weight_i = gamma(α_tier, 1) / Σ gamma(...)`, with `α = 1.0, 2.0, 3.5` for small, medium, and large restaurants.

**Meaning:** Restaurant popularity skew, normalised to sum to 1.

### F6 — Partner density
**Formula:** `density = 475,000 / 61,111 = 7.772 partners/km²`

**Meaning:** National partner density anchor.

### F7 — Partner counts per time band
**Formula:**
- `peak = density × 650 × 0.50 × 0.38 ≈ 961`
- `normal = peak × 0.565 = 543`
- `night = peak × 0.350 = 336`

**Meaning:** Partner counts per time band.

### F8 — Restaurant preparation time
**Formula:** `prep_time ~ U{low, high}` per tier: 10–15, 15–25, and 20–30 minutes.

**Meaning:** Restaurant preparation time.

---

## Stage 3: Demand Side

### F9 — National order density
**Formula:** `density = 2.36M / 61,111 = 38.65 orders/km²/day`

**Meaning:** National order density anchor.

### F10 — Base daily orders scaled to Hyderabad
**Formula:** `base orders/day = 38.65 × 650 × 3.056 × 0.50 × 0.38 × 1.09 ≈ 15,900`

**Meaning:** Base demand level for Hyderabad. It is the anchor for the hourly rates below, not the final daily total.

### F11 — Baseline hourly rate
**Formula:** `baseline/hr = 15,900 × 0.39 / 8 = 775`

**Meaning:** Fixed order rate for the 9 non-spike hours of the 10:00 to 24:00 order window.

### F12 — Peak-hour demand
**Formula:** `spike ~ U{0.90 × peak_avg, 1.10 × peak_avg} = U{1746, 2134}`

**Meaning:** Hourly rate drawn at random for the 5 spike hours (12, 13, 19, 20, 21). The expected daily total is the sum of the 5 spike draws plus 9 × 775 (about 16,900 in the run shown), and the simulated order count (16,856) comes from random order generation around those rates.

---

## Stage 4: Travel Model

### F21 — Zone travel time
**Formula:** `travel_sec[i,j] = (dist_km / 30) × 3600`

**Meaning:** Zone travel-time matrix assuming 30 km/h.

### F22 — Intra-zone travel time
**Formula:** `INTRA_ZONE_SEC = mean(0.905 × zone_radius) / 30 × 3600`

**Meaning:** Same-zone pickup or drop-off time used in the simulations.

### F23 — Distance conversion
**Formula:** `dist_km = sec / 3600 × 30`

**Meaning:** Inverse conversion for logging.

---

## Stage 5: Greedy Dispatch (`02_greedy_baseline`)

### F24 — Nearest-available assignment
**Formula:** `partner = argmin over available p of pickup_sec(p.zone → restaurant.zone)`

**Meaning:** Assigns an order to the available partner with the shortest pickup time.

### F25 — Partner busy window
**Formula:**
- `total_travel = pickup_sec + dropoff_sec`
- `return_time = t + total_travel`

**Meaning:** Defines the period during which a partner is busy.

### F26 — Target active partners
**Formula:** `target_active(h) ∈ {543, 961, 336}`

**Meaning:** Active partner target by time band.

### F27 — Cancellation window
**Formula:** `cancel_window = 600 s` (default), `480 s` (peak), `240 s` (night).

**Meaning:** Queue timeout before an order is unassigned.

### F28 — Missed-batch definition
**Formula:** Same restaurant, `t − t_prev ≤ 120 s`, and a different partner.

**Meaning:** Defines a missed batch using a sliding deque.

### F29 — Missed-batch rate
**Formula:** `missed_batch_pct = missed_count / total_dispatches × 100`

**Meaning:** Percentage of dispatches counted as missed batches.

### F30 — Fuel cost per kilometre
**Formula:** `fuel_cost_per_km = 111.21 / 40 = ₹2.780`

**Meaning:** Fuel cost per kilometre.

### F31 — Cost model
**Formula:** `cost = partners_used × 40 + total_km × 2.78`

**Meaning:** Combines partner cost and distance-based cost.

### F32 — Time-weighted partner target
**Formula:** `weighted_avg_partners = (543·n_off + 961·5 + 336·2) / (n_off + 5 + 2)`

**Meaning:** Time-weighted partner target.

### F33 — Partner utilisation
**Formula:** `utilization_% = min(100, busy_sec / sim_duration × 100)`

**Meaning:** Partner utilisation percentage.

### F34 — Per-dispatch distance
**Formula:** `total_distance = pickup_km + delivery_km`

**Meaning:** Total distance for each dispatch trip.

---

## Stage 6: ML Batching (`03_batching`)

### F35 — Haversine distance
**Formula:** `a = sin²(Δφ/2) + cosφ₁ cosφ₂ sin²(Δλ/2)`

**Distance:** `d = 6371 · 2 · atan2(√a, √(1−a))`

**Meaning:** Great-circle distance between two points.

### F36 — Missed-batch training label
**Formula:** `missed_batch_label = 1` if the order appears in any missed pair (earlier or later order).

**Meaning:** Training label for the ML model.

### F37 — Restaurant order frequency
**Formula:** `restaurant_order_freq = count(orders per restaurant × peak_window)`

**Meaning:** Feature 1.

### F38 — Queue depth
**Formula:** `queue_depth = number of orders at the same restaurant in the last 120 s`

**Meaning:** Feature 2.

### F39 — Distance to queued destinations
**Formula:** `delivery_distance_to_queued = mean haversine(current_dest, each queued_dest)`, or `0` if the queue is empty.

**Meaning:** Feature 3.

### F40 — Partner count by destination zone
**Formula:** `zone_partner_count = nunique(assigned_partner) per (dest_zone, peak_window)`

**Meaning:** Feature 4.

### F41 — Time features
**Formula:** `is_peak_hour`, `time_of_day_encoded ∈ {0..4}`

**Meaning:** Features 5 and 6.

### F42 — XGBoost class imbalance
**Formula:** `scale_pos_weight = neg_count / pos_count`

**Model settings:** 300 trees, depth 4, learning rate 0.05, and an 80/20 stratified split.

**Meaning:** Handles class imbalance in the XGBoost model.

### F43 — Live simulation decision threshold
**Formula:** Hold an order if `P(hold) > 0.6`.

**Meaning:** Decision threshold in the live simulation.

---

## Stage 7: CVRP and Eligibility

### F44 — CVRP setup
**Formula:** `n_vehicles = ⌈n_orders / capacity⌉`, with capacity = 3 and demand = 1 per order.

**Meaning:** Vehicle-routing setup.

### F45 — Integer-scaled arc cost
**Formula:** `arc_cost = int(haversine_km × 100)`

**Meaning:** Integer scaling for OR-Tools.

### F46 — Depot coordinates
**Formula:** Depot coordinates = `mean(delivery_lat, delivery_lon)` of the group.

**Meaning:** Restaurant location approximation.

### F47 — Q (ceiling): proximity eligibility
**Formula:** Batch only if all pairwise destination haversine distances are `≤ 1.5 km`.

**Meaning:** Literature-anchored proximity rule.

### F48 — P (floor): same-zone eligibility
**Formula:** Batch only if `nunique(destination_zone_id) == 1`.

**Meaning:** Zero-parameter same-zone rule.

### F49 — Batch route length
**Formula:** `delivery_only_km = Σ haversine(prev_stop → stop)` along the route.

**Meaning:** Total delivery distance along the batch route.

### F50 — Per-order cost split
**Formula:**
- `per_order_delivery = delivery_only_km / n`
- `per_order_pickup = pickup_km / n`

**Meaning:** Splits route distance across batched orders.

### F51 — Batched pair count
**Formula:** `batched_pairs = batched_count / 2`

**Meaning:** Number of batched pairs.

### F52 — Average metric
**Formula:** `avg_metric = (P + Q) / 2`

**Meaning:** Midpoint of the `[P, Q]` range.

### F53 — Improvement percentage
**Formula:** `Δ% = (smart − greedy) / greedy × 100`

**Meaning:** Measures improvement relative to greedy dispatch.

### F54 — Distance saved per batched order
**Formula:** `km_saved_per_batched_order = (greedy_km − smart_km) / batched_count`

**Meaning:** Batching distance savings per order.
