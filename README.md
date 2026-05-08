# Bayesian Hierarchical Modeling of Professional Hockey Performance

This project applies a Bayesian hierarchical model to evaluate seasonal performance across 8 professional hockey seasons using game-level net expected goals (NxG) as the primary outcome metric.

Note: This project was originally developed as part of graduate coursework in Bayesian Statistics and later refactored into a public portfolio project with improved documentation and structure.

---
## Practical Relevance

This framework can support:
- player evaluation
- contract decisions
- roster planning
- team fit analysis

---
## Project Overview

Traditional hockey statistics such as goals, assists, and points often fail to capture the full impact of a player's on-ice performance. Advanced metrics such as Expected Goals (xG), Corsi, Fenwick and others, provide stronger insight into overall contribution by accounting for shots generated, shot quality and defensive impact.

This project uses Bayesian hierarchical modeling to estimate true seasonal performance while accounting for:

- season-to-season variance
- team effects
- game-to-game randomness
- unequal seasonal variance
- partial pooling across seasons

The primary outcome performance metric analyzed is Net Expected Goals (NxG):

NxG = xGF - xGA

where,

- xGF = expected goals for while on the ice
- xGA = expected goals against while on the ice

---
## Research Questions

The analysis aims to answer:

1. Best and worst season?
2. Most and least consistent season?
3. Career consistency?
4. Team effect?

---
## Dataset

The dataset consists of 8 seasons of professional game-level perfomance data for a single player.

### Variables used

- season
- team
- NxG

Additional variables were available during preprocessing:

- time on ice
- power play time
- short-handed time
- home/away
- game result
- game score
- opposing team

Raw data are not included due to licenseing, redistribution restrictions and proprietary team analytics ownership.

---
## Modeling Approach

An iterative model-building process was followed:

### 1. ANOVA baseline

Independent season-level comparison (rejected due to lack of pooling).

### 2. Hierarchical seasonal model

Partial pooling across seasons using random effects.

### 3. Unequal variance hierarchical model

Season-specific variance estimates to capture consistency differences

### 4. Final mixed-effects hierarchical Bayesian model

- seasonal random effects
- team fixed effects
- unequal season variance
- non-cenetered parameterization for stable sampling

Implemented using:
- PyMC
- ArviZ
- NumPy
- pandas
- matplotlib

---
## Key Findings
### Season Performance
After accounting for team effects and partial pooling across seasons, no individual season showed strong posterior evidence of being significantly better or worse than the player’s overall baseline performance. All seasonal posterior credible intervals contained zero, suggesting that observed season-to-season differences were largely explained by natural variability rather than true performance shifts.

- Season 5 had the highest posterior probability of being the strongest season, being identified as the “best” season approximately 18% of the time during posterior sampling, although not statistically conclusive. 

- Season 4 had the highest posterior probability of being the weakest season, while Season 8 also showed weaker overall performance estimates. Season 5 had a 62.5% and 57.9% probability of being better than Season 4 and Season 8, respectively.

### Consistency

Consistiency was evaluated using season-specific posterior variances estimates, where a lower posterior variance estimate indicated more stable game-to-game perfomance within that season.

- Season 1 was identified as the most consistent season, appearing as the most stable in approximately 39% of the posterior samples. 

- Season 2 and Season 5 also showed strong consistency with 25% and 22% of the the posterior samples identifying them as the most consistent seasons.

- Season 8 was indentified as the least consistent season approximately 38% of the time during posterior sampling.

- Game-level variability within seasons was substantionally larger than career-level variability, indicating that game-by-game fluctuations were much greater than career performance.


### Team Effect

A meaningful posterior difference between teams was observed after controlling for season-level effects. The model estimated that Team 1 was associated with improved player performance relative to Team 2, with the posterior contrast excluding zero.

This suggests that team context, such as system fit, usage, teammates, coaching, and deployment, may have had a measurable impact on performance outcomes.

Team changes were tied to different career periods, so this result should be interpreted as an association rather than a strictly causal team effect.

### Overall Conclusion

Performance across seasons was generally stable, with no strongly dominant “best” or “worst” season after accounting for uncertainty and team effects. Season 5 emergeed as the strongest candidate for the best season and Season 8 showed the greatest inconsistency, but not statistically decisive.

Team environment showed a stronger influence on observed performance than individual seasonal variation alone.

This highlights the importance of using Bayesian hierarchical modeling in sports analytics, where uncertainty, partial pooling, and contextual effects are often more informative than raw summary statistics alone or isolated seasonal comparisons.

---
## Visualizations

- posterior seasonal estimates
- posterior team estimates
- posterior seasonal variance estimes

---
## Future Improvements

Several extensions could provide a more complete performance analysis:

- **Informed priors:** Stronger priors for seasonal effects and season-specific variance estimates based on domain knowledge of expected performance levels and consistency.

- **League-wide baseline comparison:** Expand the dataset to include additional players across the league to better estimate team effects and evaluate performance relative to a broader league baseline rather than a single-player career average.

- **Team–season interaction effects:** Introduce an interaction term between season and team to determine whether specific team-season combinations had a stronger influence on performance outcomes.

- **Usage-based performance modeling:** Include deployment variables such as Time on Ice (TOI), Power Play Time on Ice (PPTOI), and Short-Handed Time on Ice (SHTOI) to better account for how role and usage affected game-level performance.

---
## Repository Strucutre

---
## How to Run

---
## License

MIT license

---
## Author

Alex Wall



This repository is shared for portfolio and educational purposes and is not intended for direct academic submission.
