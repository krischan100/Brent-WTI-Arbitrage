## Overview

In this project, I analyse potential **transatlantic arbitrage opportunities** between **Brent (Europe)** and **WTI (U.S.)** crude oil benchmarks using historical market data from Yahoo Finance. The idea behind this study is simple but mirrors what happens in real physical oil trading.

In the physical market, oil can be bought in Europe under the **Brent** benchmark and shipped across the Atlantic to the **United States**, where it can be sold under the **WTI** benchmark. If the price differential between WTI and Brent is wide enough to cover freight and related costs, the trader can lock in a profit — this is the essence of a **geographical arbitrage**.

This notebook models that relationship using only the benchmark prices and a **fixed shipping cost**. It calculates monthly profit per barrel as:

**Actual Transaction Price = Benchmark Price + Differential**

I then visualise which months would have presented profitable arbitrage opportunities between 2020 and 2025.

---

## Data & Methodology

- **Data source:** Yahoo Finance  
  - WTI: `CL=F`  
  - Brent: `BZ=F`  
- **Period:** January 2020 – September 2025  
- **Frequency:** Monthly (end-of-month close)  
- **Assumed freight rate:** \$2.50 per barrel (Europe → U.S.)

The model identifies profitable months where the WTI price exceeded Brent by more than the assumed freight cost. The visualisation shades these periods green (profitable) and red (unprofitable).

---

## Physical-World Context

In reality, this kind of arbitrage sits within a much larger trading chain:

**Producer → Trader  → Refinery **

Oil is not sold directly as “Brent” or “WTI.” These are **benchmarks** — reference prices representing standardised grades at specific delivery locations:
- **WTI**: Cushing, Oklahoma  
- **Brent**: North Sea (Sullom Voe or Rotterdam basis)

Each physical cargo trades as:

\[
\text{Actual Transaction Price} = \text{Benchmark Price} + \text{Differential}
\]

The **differential** reflects real-world adjustments for:
- Crude quality (sulfur content, API gravity)  
- Location (distance from benchmark delivery point)  
- Timing (month of delivery)  
- Regional market tightness or oversupply  

My simplified model ignores these additional factors and isolates only the headline **benchmark differential** and **freight**, to give a clean, transparent picture of the fundamental arbitrage dynamics.

---

## Improvements & Realistic Extensions

In a true trading environment, many other costs and risks would affect the economics of a cargo move:

- **Variable freight rates:** Actual dirty-tanker charter rates fluctuate daily based on vessel availability, distance, and bunker fuel prices.  
- **Insurance:** Around \$0.10–\$0.20 per barrel for transit coverage.  
- **Financing:** Interest and letters of credit for multi-million-dollar cargoes in transit.  
- **Port and handling fees:** Loading, unloading, and storage costs.  
- **Taxes and regulatory costs:** Depending on jurisdiction and route.  
- **Risk premium:** Compensation for market volatility, counterparty risk, and geopolitical factors.

Due to limited access to reliable freight and insurance data, I use a **fixed freight rate of \$2.50/bbl**, which is broadly realistic for Europe–U.S. Aframax tanker routes under normal market conditions. Future versions could integrate live freight indices (e.g. Baltic Dirty Tanker Index) or real-world differentials to better approximate commercial reality.

---

## Key Takeaways

- WTI–Brent spreads fluctuate significantly month-to-month, occasionally exceeding realistic freight rates.  
- Such movements reflect **regional supply and demand imbalances** — for instance, pipeline constraints in the U.S. or production outages in the North Sea.  
- Even a simplified analysis provides insight into how traders like **Glencore, Vitol, or Trafigura** identify arbitrage windows and deploy tankers accordingly.

---

## Project Summary

- **Language:** Python  
- **Libraries:** `pandas`, `yfinance`, `matplotlib`, `numpy`  
- **Focus:** Identifying historical arbitrage windows between Brent and WTI crude benchmarks  
- **Goal:** Demonstrate understanding of physical oil trading economics and price relationships through reproducible data analysis
