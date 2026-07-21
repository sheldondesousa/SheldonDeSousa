# ⚽ World Cup Prediction Model

An AI-assisted experiment testing mathematical models (Elo ratings + Poisson distributions) to predict match outcomes using a data pipeline via Kaggle.

Repo: [FIFA-Prediction-Model](https://github.com/sheldondesousa/FIFA-Prediction-Model)

---

# World Cup Predictor

Predicts the most likely World Cup winner from historical data, and shows the quantitative evidence behind the prediction — not just a name.

Given a live or upcoming tournament bracket, it simulates the rest of the tournament thousands of times using Elo ratings and Poisson-distributed goal scoring, then reports each remaining team's title probability along with the evidence behind it (Elo gap, simulated win rate, historical base rate at that stage).

## Approach

1. Convert the Elo rating gap between two teams into win/draw/loss probabilities
2. Convert those into expected goals via a Poisson distribution, calibrated on historical goals-per-match at each rating gap
3. Simulate matches (and the bracket they feed into) using those distributions
4. For knockout rounds, simulate extra time and penalties using historical shootout rates
5. Roll the simulation forward through the remaining bracket 10,000+ times and count how often each team wins — that frequency is the reported probability

This is the same family of method (Elo + Poisson Monte Carlo) behind most credible public World Cup forecasts. It's deliberately not a deep learning model — with only 22 past World Cups to learn from, a black-box model would both overfit and undermine the "show your evidence" goal.

## Status

v1 working: Elo rating engine, Poisson goal-simulation model, knockout bracket Monte Carlo simulator, historical backtest, a custom "Match Outlook" web app, and a Streamlit app.

## Data sources

- [Kaggle: International football results from 1872 to 2024](https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017) — match-level historical results
- [eloratings.net](https://www.eloratings.net/) — historical Elo ratings for national teams
- FIFA's official World Rankings archive

## Roadmap

- **v1:** Elo + Poisson simulation, static historical bracket backtest, Streamlit display for the current tournament's knockout stage
- **v2:** Knockout-stage-experience adjustment, full backtesting/evaluation suite, published calibration numbers
- **v3:** Extend to simulate from a full pre-tournament field, not just mid-tournament
