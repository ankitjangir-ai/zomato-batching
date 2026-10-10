# Limitations

1. **Synthetic cities, not real data.** Orders, restaurants and partners are generated from published figures. No Zomato internal data was used.
2. **Unknown dispatch logic.** I cannot see Zomato's real dispatch rules, so I cannot say why orders like the three that started this project were not batched. The greedy baseline is my model of the current behaviour, not a copy of it.
3. **The motivating example is one anecdote.** Three orders show the pattern is possible, not that it is common.
4. **Batching assumptions.** Results depend on the eligibility rule. Q combines orders whose destinations are within 1.5 km, a threshold anchored to a food-delivery batching patent example. P combines only orders in the same zone, an assumption made for this project. Different thresholds or rules would change the results.
5. **Generated destinations.** Delivery destinations are generated, not observed. In Hubli-Dharwad, 75% of orders are delivered within the restaurant's own zone; in Hyderabad the figure is 90%. In both cities, 90% of the remaining cross-zone orders go to nearby zones. These shares are assumptions, and different values would change how often orders can be batched.
6. **Service quality.** Orders carry delivery-deadline and preparation-time fields, but the batching rules do not enforce them, and the model does not measure delivery time, food freshness or customer experience. Batching is judged on partners used, distance and cost only.
7. **Single national petrol price** is used for both cities, which is less accurate locally.
8. **Two cities only.** Extending to the whole country multiplies the uncertainty.
9. **National figures are projections,** not forecasts.
10. **Partner effects.** Savings are described as improved utilisation. The model does not cover partner earnings or incentives beyond the fixed-plus-variable cost model.
