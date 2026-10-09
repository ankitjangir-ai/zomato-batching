# Motivation: Why I Built This

One evening, my two friends and I decided to skip the mess dinner and order food instead. We were walking around the campus and planned to order at the same time from the **same restaurant**, to the **same destination**. The three orders were placed between **8:21 and 8:23 PM**, within about two minutes of each other.

When the orders arrived, I noticed something odd. Even though the restaurant and the destination were the same and the timing was nearly the same, **Zomato had assigned three separate delivery partners**. Three riders had picked up from the same place and travelled to the same place, which means more petrol burned, more pollution, and more cost for the company, if one rider could have carried all three.

The bills for all three orders are in [`evidence/`](evidence/), with personal details redacted.

## The connection to Zomato's finances

As a personal interest, I had been reading the annual reports of several companies over time, Eternal among them. In those reports I saw that Zomato became profitable for the first time in FY24, and that its profit grew further in FY25. The FY26 report shows profit settling lower, at about ₹366 crore against ₹527 crore in FY25, so margins are still thin and efficiency matters.

That made me ask a question: **could delivery inefficiency like this affect Zomato's profitability, and if so, by how much?**

## The project

To find out, I built two synthetic cities using official data from the Zomato segment of Eternal's annual reports for FY24, FY25 and FY26:

- **Hyderabad** (Tier 1)
- **Hubli-Dharwad** (Tier 2)

In each city I simulated how orders are currently dispatched, tested smarter batching methods, and measured the difference in distance, cost and emissions. The goal was to understand how the current system works and what could optimise it.

## What this does and doesn't show

My three orders are what started the project, but they are not proof on their own. I can't see Zomato's internal dispatch logic, so I don't know why those orders weren't batched. There may be good reasons, such as partner availability, food preparation times, or batching rules I can't see. The simulation exists to test whether the pattern could matter at scale, using assumptions and officially published figures rather than Zomato's internal data.
