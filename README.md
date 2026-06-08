# information-theoretic-investing

A research repository for framing investing and trading as an information problem rather than only a price or factor problem. This repo centers on KL divergence, calibrated forecasts, market-implied distributions, Kelly growth, and the practical idea of measuring edge in **nats per day**. [page:1]

## What this is

This repository is an early home for notes, specs, and future code around **information-theoretic investing**. The basic idea is that a trading or investing edge can be described as the divergence between an investor's forecast distribution and the market's implied distribution, with performance understood through log growth and information capture. [page:1]

## Core idea

In plain terms:

- The market implies a probability distribution through prices.
- A trader or investor has their own forecast distribution.
- The gap between the two can be measured with KL divergence.
- That gap can be interpreted as information edge.
- Over time, that edge can be expressed as a rate, such as `nats per day`. [page:1]

This repo is meant to be a working place for turning that framing into a usable research program. [page:1]

## Main file

The most important file right now is [`llms.txt`](./llms.txt). It is a model-facing specification that explains the conceptual framework, provenance, and intended interpretation of terms like “investing is compression,” “KL divergence as edge,” and “0.0209 nats per day.” [page:1]

## Why publish this now

Publishing this now creates a canonical public location for the idea as it develops. It also makes the framework easier to reference, extend, and build on across notes, code, and AI-assisted research workflows. [page:1]

## Planned additions

Likely future additions include:

- Notes on estimating market-implied distributions
- Forecast calibration methods
- Examples of KL-based edge calculations
- Position sizing and Kelly-style implementations
- Regime comparisons across asset classes
- Notebooks, simulations, and empirical tests [page:1]

## Repository structure

Current / intended structure:

- `README.md` — overview of the repo
- `llms.txt` — model-facing conceptual spec
- `notes/` — research notes and drafts
- `notebooks/` — experiments and simulations
- `data/` — sample or derived datasets
- `src/` — code for models, estimation, and backtests [page:1]

## Status

This is an early-stage research repository. The framework is live, but the codebase and empirical layer are still being developed. [page:1]

## Author

Jonah Faulkner [page:1]
