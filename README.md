# IntraDay_VWAP_Algorithm

Intraday VWAP Sell Execution
This notebook answers a practical execution question: how should an order equal to 10% of a stock's daily market volume be sold during one trading day?

It downloads intraday data from yfinance, builds a historical intraday volume curve for planning, and simulates a VWAP-style sell schedule. The backtest uses realised volume, so it can show whether a strict participation limit would have completed the order.

Execution logic
Let Q be the shares to sell, V be the session's market volume, and v_t be volume in bar t. For an order that is 10% of daily volume, Q = 0.10 * V. A VWAP schedule distributes it in proportion to market volume:

q_t = Q * v_t / V = 0.10 * v_t

So the strategy sells 10% of each 5-minute bar. If the order fraction equals the maximum participation rate, there is no spare capacity to catch up later; execution must track volume continuously. The historical curve is useful before the session, while realised bars are used here to evaluate the schedule.
