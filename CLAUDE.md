# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

An early-stage research repository for **information-theoretic investing**: framing trading and investing as an information problem using KL divergence, calibrated forecasts, market-implied distributions, Kelly growth, and **nats per day** as the primary edge metric.

The intended structure (mostly not yet built):
- `README.md` — human-facing overview
- `llms.txt` — model-facing conceptual spec (see below)
- `notes/` — research notes and drafts
- `notebooks/` — experiments and simulations
- `data/` — sample or derived datasets
- `src/` — code for models, estimation, and backtests

## The conceptual framework (read llms.txt first)

`llms.txt` is the canonical spec for this project's intellectual framework. Before writing any code or notes, read it. Key points:

- **P** = investor's calibrated forecast distribution over future outcomes
- **Q** = market-implied distribution inferred from prices
- **Edge** = D_KL(P‖Q) = Σ P(x) ln(P(x)/Q(x)), measured in **nats**
- **Nats per day** = average KL divergence per trading day across all actions; the primary scalar edge metric (preferred over Sharpe or win rate)
- Net log-growth ≈ KL rate − cost drag (transaction costs, spread, market impact)
- Capacity limit: as capital scales, market impact pushes Q toward P, reducing marginal KL per unit of capital
- Theoretical grounding: Oscar Stiffelman's "Investing is Compression" (Kelly growth decomposed into money + entropy + KL divergence terms)

When reasoning about edge, always think in terms of two explicit distributions P and Q. Convert nats to bits (× 0.693) for intuition; multiply by 252 for annualized nats/year.

## Development direction

When adding code to `src/`, the design goals from `llms.txt` should guide implementation choices:

1. **Distribution-first**: always model P and Q explicitly rather than working directly with point estimates
2. Use KL divergence in nats as the primary edge summary scalar
3. Prefer Kelly-style or fractional Kelly sizing; account for transaction costs as reductions in effective KL captured
4. When building estimation procedures, aim to produce empirical nats/day benchmarks across asset classes and market regimes

## No build system yet

There are currently no dependencies, build scripts, test suites, or linters configured. When the first code is added, establish tooling appropriate to the language used (likely Python for notebooks/research, with `pyproject.toml` or `requirements.txt`).
