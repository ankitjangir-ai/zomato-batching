# Limitations

1. **Synthetic cities, not real data.** Orders, restaurants and partners are generated from published figures. No Zomato internal data was used.
2. **Unknown dispatch logic.** I cannot see Zomato's real dispatch rules, so I cannot say why orders like the three that started this project were not batched. The greedy baseline is my model of the current behaviour, not a copy of it.
3. **The motivating example is one anecdote.** Three orders show the pattern is possible, not that it is common.
4. **Batching assumptions.** A 0.5 km destination limit and a generated destination pattern (20% identical, 80% nearby) drive the results. Different assumptions would change them.
5. **Service quality.** [State how delivery time and food quality were handled, and what the model does not capture, such as preparation time differences.]
6. **Single national petrol price** is used for both cities, which is less accurate locally.
7. **Two cities only.** Extending to the whole country multiplies the uncertainty.
8. **National figures are projections,** not forecasts.
9. **Partner effects.** Savings are described as improved utilisation. The model does not cover partner earnings or incentives beyond the fixed-plus-variable cost model.
