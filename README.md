# Optimal Stopping via Monte Carlo Simulation

## Overview

This project studies **optimal stopping problems** for stochastic processes using Monte Carlo simulation.

Given a stochastic process $(X_t)_{t \ge 0}$ and a payoff function $g$, the goal is to determine when it is optimal to stop the process in order to maximize expected payoff. Rather than relying on closed-form solutions, this project focuses on **computational exploration** of stopping regions and value functions.

The emphasis is on:

* understanding the **structure of stopping rules**,
* visualizing **stopping vs continuation regions**, and
* examining how these regions depend on model parameters.

This project is intended as an applied probability and stochastic control study, not a financial pricing exercise.

---

## Mathematical Formulation

We consider optimal stopping problems of the form

$$V(x) = \sup_{\tau \in \mathcal{T}} \mathbb{E}_x \big[ g(X_\tau) \big],$$

where:

* $(X_t)_{t \ge 0}$ is a stochastic process,
* $\tau$ is a stopping time with respect to the natural filtration of $X_t$,
* $g : \mathbb{R} \to \mathbb{R}$ is a payoff function.

The objective is to approximate the value function $V(x)$ and infer the **optimal stopping rule**.

---

## Stochastic Model

The primary model studied is **Geometric Brownian Motion (GBM)**:

$$dX_t = \mu X_t \, dt + \sigma X_t \, dW_t,$$

where:

* $\mu$ is the drift,
* $\sigma$ is the volatility,
* $W_t$ is standard Brownian motion.

The process is simulated using an exact discretization of GBM on a finite time horizon $[0,T]$.

Extensions to other processes (e.g. mean-reverting diffusions) are discussed.

---

## Payoff Structure

We focus on a threshold-type payoff function:

$$g(x) = \max(x - K, 0),$$

where $K$ is a fixed level.

This payoff induces a nontrivial trade-off between:

* stopping early to secure payoff,
* continuing to benefit from future stochastic growth.

The resulting optimal stopping rule exhibits a **time-dependent stopping boundary**, which is the primary object of study.

---

## Numerical Method

The optimal stopping problem is approximated using a **backward induction Monte Carlo algorithm**:

1. Simulate a large number of sample paths of $X_t$.
2. Discretize time into a finite grid.
3. At each time step, compare:
   * the immediate payoff $g(X_t)$,
   * an estimated continuation value based on future simulated payoffs.
4. Stop whenever the immediate payoff exceeds the continuation value.

This procedure approximates the dynamic programming principle underlying optimal stopping.

---

## Experiments and Analysis

The project investigates:

* Empirical stopping regions in the $(t,x)$-plane
* Sample paths with stopping times highlighted
* Sensitivity of stopping boundaries to:
  * volatility $\sigma$,
  * drift $\mu$,
  * time horizon $T$
* Stability of results with respect to discretization and number of paths

The focus is on **qualitative structure**, not closed-form accuracy.

---

## Limitations and Extensions

This study is purely simulation-based and does not attempt to solve the associated free-boundary PDE analytically.

Possible extensions include:

* alternative payoff functions,
* mean-reverting processes,
* connections to Hamilton–Jacobi–Bellman equations,
* numerical stability analysis of stopping boundaries.

---

## Project Goals

This project aims to demonstrate:

* independent exploration of stochastic processes,
* applied understanding of stopping times and dynamic programming,
* computational intuition for problems arising in probability and control.

It is designed as a research-style applied mathematics project.
