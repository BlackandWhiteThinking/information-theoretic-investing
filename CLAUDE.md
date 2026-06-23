# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A research project exploring how trading and investing can be understood as an information problem — asking "how much does the investor know that the market doesn't?" — rather than purely a price or risk problem.

The intended structure (mostly not yet built):
- `README.md` — human-facing overview
- `llms.txt` — model-facing conceptual spec (see below)
- `notes/` — research notes and drafts
- `notebooks/` — experiments and simulations
- `data/` — sample or derived datasets
- `src/` — code for models, estimation, and backtests

## The conceptual framework (read llms.txt first)

`llms.txt` is the canonical spec for this project's intellectual framework. Read it before writing any code or notes. Key ideas in plain terms:

The project centers on comparing two probability distributions — a spread of guesses about what might happen and how likely each outcome is:

- **P** (jargon: *the investor's calibrated forecast distribution*) — the investor's own view of the odds of different outcomes
- **Q** (jargon: *the market-implied distribution*) — what the market's current prices imply about the odds of those same outcomes

The gap between P and Q is the investor's **edge** — how much they know that the market hasn't priced in yet. This gap is measured with a formula called **KL divergence** (jargon: *Kullback–Leibler divergence*, written D_KL(P‖Q)), which produces a number in units called **nats** (jargon: *natural-log information units*; 1 nat ≈ 1.44 bits).

That gap, averaged over a trading day, gives **nats per day** (jargon: *the KL rate*) — the project's primary way of scoring edge. It is preferred over conventional metrics like Sharpe ratio or win rate because it directly measures information advantage rather than a side-effect of it.

Actual returns are less than the raw edge because of **cost drag** (jargon: *transaction costs, spread, and market impact*). So: net growth ≈ nats per day − cost drag. As a strategy grows in size, trading it moves prices, which shrinks the gap between P and Q and reduces the edge — this is the **capacity limit** (jargon: *market impact reducing marginal KL per unit of capital*).

The theoretical grounding comes from Oscar Stiffelman's "Investing is Compression," which shows that **Kelly growth** (jargon: *log-optimal portfolio growth, the reinvestment rate that maximises long-run wealth*) can be broken into three parts: a money term, an entropy term, and a KL divergence term.

To convert between units: nats × 0.693 = bits; nats/day × 252 = annualised nats/year.

## Development direction

When adding code to `src/`, let the design goals from `llms.txt` guide decisions:

1. Always work with two explicit probability distributions (P and Q) rather than collapsing to a single point estimate
2. Use nats per day as the primary summary number for edge
3. Size positions using **Kelly or fractional Kelly** (jargon: *bet-sizing rules derived from log-growth maximisation*); explicitly subtract transaction costs from the effective edge captured
4. Build toward producing empirical nats/day benchmarks for different asset classes and market conditions

## No build system yet

There are currently no dependencies, build scripts, test suites, or linters configured. When the first code is added, establish tooling appropriate to the language used (likely Python for notebooks/research, with `pyproject.toml` or `requirements.txt`).
