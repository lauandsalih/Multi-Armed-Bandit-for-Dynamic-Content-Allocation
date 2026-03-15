# Multi-Armed Bandit for Dynamic Content Allocation

## Overview
This project replaces traditional, static A/B testing with a dynamic **Multi-Armed Bandit (MAB)** algorithm using **Thompson Sampling**. By applying Bayesian probability, the algorithm continuously learns which website variation or advertisement has the highest conversion rate and actively funnels more traffic to the winning variation in real-time.

## The Mathematical Model
The algorithm uses **Bayesian Updating** and **Beta Distributions** to model the uncertainty of each variation's true conversion rate.

### 1. The Prior
We assume the probability of a user converting (clicking, buying) for variation $k$ follows a Beta distribution. Before the test starts, we have no information, so we use a uniform prior:
$$P(\theta_k) \sim \text{Beta}(\alpha=1, \beta=1)$$

### 2. The Posterior Update
As users interact with the site, we observe successes (conversions) and failures (bounces). Because the binomial likelihood and the Beta distribution form a conjugate prior relationship, updating our belief is computationally trivial. 

If we observe $S$ successes and $F$ failures for variation $k$, the new posterior distribution becomes:
$$P(\theta_k \mid \text{Data}) \sim \text{Beta}(\alpha + S, \beta + F)$$

### 3. Thompson Sampling (Action Selection)
For every new user that arrives, the algorithm samples a random value from the current Beta distribution of each variation. It serves the user the variation that generated the highest sampled value:
$$a_t = \arg\max_k \left[ \theta_k \sim \text{Beta}(\alpha_k, \beta_k) \right]$$

Because narrower distributions (higher certainty) sample closer to their true mean, and wider distributions (high uncertainty) have a chance of sampling high values, the algorithm naturally balances **Exploration** (testing uncertain variations) with **Exploitation** (capitalizing on known winners).

## Business Value
In traditional A/B/n testing, traffic is split equally. This results in high "Regret"—the lost revenue from intentionally sending users to inferior variations just to achieve statistical significance. 

By dynamically shifting traffic via Thompson Sampling, this script demonstrates how a company can capture significantly more conversions *during* the testing phase, optimizing user experience and maximizing revenue without waiting weeks for an A/B test to conclude.

## Technologies Used
* **Python**
* **NumPy / SciPy** (For Beta distribution sampling and binomial simulations)


