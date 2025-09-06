---
layout: post
title: "Why Convexity Grows Rapidly with Term of Cashflows"
date: 2025-09-06
tags: [pensions, fixed-income, convexity, term-structure]
math: true
toc: true
---

## Introduction

A common question in fixed-income analysis is:  
**Why does convexity increase so strongly as the term of cashflows lengthens?**

This matters particularly for pension funds, since liabilities with very long maturities have disproportionately high convexity compared to asset portfolios.

---

## Setup

Let $y$ be the continuously compounded yield. A bond (or liability) with positive cashflows $\{CF_i\}$ at times $\{t_i\}$ has price:

$$
P(y) = \sum_i CF_i \, e^{-y t_i}.
$$

Define **pricing weights**:

$$
p_i(y) \equiv \frac{CF_i e^{-y t_i}}{P(y)}, 
\quad p_i > 0, \quad \sum_i p_i = 1.
$$

Then:

- **Modified duration**:
  $$
  D_{\text{mod}}(y) = \sum_i p_i \, t_i = \mathbb{E}[t].
  $$

- **Convexity**:
  $$
  C(y) = \sum_i p_i \, t_i^2 = \mathbb{E}[t^2].
  $$

Thus duration is the weighted mean of payment times, and convexity is the weighted **second moment** of payment times.

A key identity follows:

$$
C - D_{\text{mod}}^{\,2} = \mathbb{E}[t^2] - (\mathbb{E}[t])^2 = \mathrm{Var}(t) \ge 0.
$$

---

## Zero-Coupon Bond: Quadratic Growth

For a single payment at time $T$:

$$
P = e^{-yT}, 
\qquad D_{\text{mod}} = T, 
\qquad C = T^2, 
\qquad \frac{dC}{dT} = 2T.
$$

Convexity grows **quadratically** in maturity. The marginal increase $dC/dT$ itself grows linearly with $T$.

---

## General Cashflow: Magnification of Late Payments

Because $C = \mathbb{E}[t^2]$:

- A dollar of (PV-weighted) cashflow at time $t$ contributes $\propto t^2$.  
- Moving weight further out increases $t^2$ disproportionately.

**Local shift lemma:**  
Move a small PV weight $\varepsilon$ from time $s$ to time $s+\Delta$. Then:

$$
\Delta C = \varepsilon \big[(s+\Delta)^2 - s^2\big] = \varepsilon \,(2s\Delta + \Delta^2) > 0.
$$

For large $s$, the linear term $2s\Delta$ dominates.  
**Even a small outward shift causes a large increase in convexity.**

---

## Bounds with Maturity

Let $T_{\max} = \max_i t_i$. Then:

$$
D_{\text{mod}}^{\,2} \;\le\; C \;\le\; T_{\max}\, D_{\text{mod}}.
$$

- Lower bound: convexity always exceeds squared duration (variance).  
- Upper bound: grows with $T_{\max}$.

Thus, **longer maturities expand the feasible convexity range**.

---

## Continuous Cashflow (Annuity) Example

With continuous level cashflow $c$ over $[0,T]$:

$$
P = c \int_0^T e^{-yt}\,dt = \frac{c}{y}\,(1-e^{-yT}).
$$

The numerator of convexity:

$$
\int_0^T t^2 e^{-yt}\,dt
= \frac{2}{y^3} - e^{-yT}\!\left(T^2 + \frac{2T}{y} + \frac{2}{y^2}\right).
$$

So:

$$
C(T) = \frac{\tfrac{2}{y^3} - e^{-yT}\!\left(T^2+\tfrac{2T}{y}+\tfrac{2}{y^2}\right)}{\tfrac{1}{y}(1-e^{-yT})}.
$$

- For **moderate $T$** ($T \lesssim 1/y$), polynomial terms dominate → convexity rises rapidly with $T$.  
- As $T \to \infty$, discounting dominates and $C(T) \to 2/y^2$.

---

## Convex Order Argument

If $t'$ is more back-loaded than $t$ in the convex order, then:

$$
C' = \mathbb{E}[t'^2] \;\ge\; \mathbb{E}[t^2] = C.
$$

So **any mean-preserving spread of cashflows strictly increases convexity**.

---

## Takeaways

- **Zero-coupon:** $C = T^2$ (quadratic growth).  
- **General case:** $C = \mathbb{E}[t^2]$, late payments magnified.  
- **Bounds:** $D^2 \le C \le T_{\max} D$ show scaling with maturity.  
- **Annuity:** rapid convexity growth, then eventual flattening as $T \to \infty$.  
- **Implication:** Liabilities with far-out payments carry **disproportionately large convexity**, explaining why pension liabilities dominate assets in convexity terms.
