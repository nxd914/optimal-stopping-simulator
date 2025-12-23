# Optimal Execution Simulator

A stochastic simulation framework for analyzing execution costs under different trading policies.

## Overview

This project studies optimal execution as a stochastic control–inspired problem by simulating execution costs under different trading strategies in a random price environment.

Rather than focusing on point estimates or backtests, the emphasis is on distributional analysis: how execution strategies perform across many stochastic realizations of market prices.

The framework is inspired by classical execution models such as Almgren–Chriss and is intended as a numerical and methodological exploration, not a closed-form optimization solution or a live trading system.

---

## Mathematical Setup

### State and Control Variables

The system is modeled as a controlled stochastic process with:

* **State variables**: price $P_t$ and inventory $I_t$
* **Control variable**: trading rate $u_t$

The trader's objective is to choose $u_t$ to manage the trade-off between execution cost, market impact, and inventory risk over a finite horizon.

### Price Dynamics

The mid-price follows a stochastic differential equation:

$$dP_t = \mu \, dt + \sigma \, dW_t$$

which is simulated numerically using the Euler–Maruyama scheme.

Here, $\mu$ denotes drift, $\sigma$ volatility, and $W_t$ a standard Brownian motion.

### Inventory Dynamics

Inventory evolves deterministically under the trading rate $u_t$:

$$I_{t+1} = I_t - u_t \Delta t$$

In the current implementation, trading policies are fixed (time-independent), allowing isolation of structural execution trade-offs.

### Execution Cost Functional

Total execution cost is defined as:

$$\sum_t \left( u_t P_t + \eta u_t^2 + \lambda I_t^2 \right) \Delta t$$

where:

* $u_t P_t$ represents execution at stochastic prices,
* $\eta u_t^2$ captures quadratic market impact,
* $\lambda I_t^2$ penalizes inventory risk.

This functional encodes the classical tension between trading quickly (high impact) and trading slowly (inventory exposure).

---

## Methodology

For each trading policy:

1. A deterministic inventory trajectory is generated.
2. Thousands of independent price paths are simulated.
3. Total execution cost is computed for each realization.
4. Policies are compared using cost distributions, not single-point metrics.

Evaluation focuses on:

* Mean execution cost
* Standard deviation
* Upper-tail quantiles (execution risk)

This distribution-level analysis reflects how execution strategies are assessed in both research and practice.

---

## Results (Current Scope)

In a zero-drift environment ($\mu = 0$) with quadratic impact:

* Slower trading strategies reduce expected execution cost and tail risk.
* Faster trading strategies incur higher market impact costs but reduce inventory exposure time.

These outcomes are consistent with theoretical intuition and serve as validation of the simulation framework.

---

## Theoretical Context

From a theoretical perspective, this execution problem admits a Hamilton–Jacobi–Bellman (HJB) formulation arising from stochastic control.

This project does not attempt to solve the HJB equation numerically. Instead, it focuses on:

* Constructing the underlying controlled stochastic system
* Evaluating fixed policies via Monte Carlo simulation
* Studying distributional properties of execution cost

This separation mirrors common research workflows, where simulation and structural analysis precede full optimization.

---

## Scope and Limitations

This framework is designed for structural and methodological analysis, not live deployment.

Specifically:

* Price dynamics and impact models are stylized rather than calibrated to real limit order book data.
* Trading policies are fixed and non-adaptive.
* No numerical PDE or HJB solver is implemented.

These choices are intentional, allowing controlled investigation of execution trade-offs in a clean setting.

---

## Possible Extensions

* Time-dependent or adaptive trading policies
* Stronger inventory risk regimes
* Nonzero price drift or stochastic volatility
* Numerical solution of the associated HJB equation
* Mean-field or multi-agent execution models
* Calibration to empirical market microstructure data

---

## Motivation

The goal of this project is to demonstrate:

* Applied probability via Monte Carlo simulation
* Control-theoretic intuition in financial systems
* Distribution-level reasoning under uncertainty
* Research-oriented software structure

The repository is intended as a foundation for further applied mathematics or quantitative finance research.
