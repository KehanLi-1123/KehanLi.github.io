---
title: "Daily PnL of a Futures Position"
date: 2025-08-27
author: Kehan Li
---

Futures contracts are **marked-to-market daily**. This means your profit and loss (PnL) is not calculated directly from the underlying stock price, but from the **futures settlement price** each day.

---

## Key Principle

**PnL = Change in futures price × Contract size × Position direction**

- Long position → PnL is positive when futures price goes up.  
- Short position → PnL is positive when futures price goes down.  
- Settlement happens daily in your margin account.

---

## Example: 5-Day Futures Position

- 1 futures contract, multiplier = 1  
- Initial stock price = **100**  
- Initial futures price = **101** (slightly above spot because of carry costs)  
- Expiry: 5 days later  

| Day | Stock Price | Futures Price | Daily PnL (long) | Cumulative PnL |
|-----|-------------|---------------|------------------|----------------|
| 0 (entry) | 100 | 101.0 | 0.0  | 0.0  |
| 1 | 110 | 111.5 | +10.5 | +10.5 |
| 2 | 108 | 109.2 | −2.3  | +8.2  |
| 3 | 95  | 96.0  | −13.2 | −5.0  |
| 4 | 97  | 98.1  | +2.1  | −2.9  |
| 5 (expiry) | 102 | 102.0 | +3.9  | +1.0  |

---

## Observations

- **PnL is based on futures**, not the stock itself.  
- Stock and futures prices move closely but not identically (because of carry: interest rates, dividends, funding).  
- At expiry, **futures = spot price**.  
- Final cumulative PnL = **102 − 101 = +1**, even though stock moved from 100 → 102.  

---

## Why Not Use Stock Price?

- A futures contract is a **derivative agreement**, not ownership of stock.  
- Daily settlement is done by the exchange at the **futures settlement price**.  
- The stock is only relevant because the futures price is linked to it through arbitrage.  

---

## Extension: Margin Accounts (Optional)

In reality, exchanges require an **initial margin** deposit.  
- Each day, your PnL is credited/debited as **variation margin**.  
- If your margin balance falls below the **maintenance margin**, you face a **margin call**.  

This ensures the futures market has no counterparty risk: all daily gains and losses are realized immediately.
