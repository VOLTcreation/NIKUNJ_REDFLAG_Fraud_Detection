# RedFlag: Comprehensive SQL Fraud Detection Engine

## Project Overview & Tech Stack
This project is a robust anomaly detection engine built entirely in SQL to analyze a simulated fintech dataset (PayFast) containing over 200,000 transactions. The objective was to identify 12 distinct money-laundering and fraud signatures without relying on external machine learning libraries.

*   **Database Environment:** MySQL Workbench
*   **Core Language:** Pure SQL
*   **Advanced Techniques:** Common Table Expressions (CTEs), Window Functions (`LAG`, `ROW_NUMBER`, `UNBOUNDED PRECEDING`), and Correlated Subqueries (`EXISTS`).

## The 12 Fraud Signatures Analyzed

**Tier 1: Foundational Anomalies**

**1. Velocity Fraud:** Isolated accounts processing an unnatural volume of 30+ daily transactions.
![Pattern 1 Suspects]<img width="323" height="596" alt="Screenshot 2026-09-08 231725" src="https://github.com/user-attachments/assets/c331f3ef-b8ce-4390-ada5-d17d48db0582" />


**2. Round-Amount Clustering:** Flagged users with 15+ clean, round-number transactions, a classic money-laundering signature.
![Pattern 2 Suspects](<img width="453" height="630" alt="Screenshot 2026-09-08 231929" src="https://github.com/user-attachments/assets/97e83069-051d-4846-ae0c-e09b4e0377ac" />
).

**3. Card Testing:** Caught accounts executing 30+ micro-transactions (under ₹10) to validate stolen credit card lists.
![Pattern 3 Suspects](<img width="510" height="514" alt="Screenshot 2026-09-08 232055" src="https://github.com/user-attachments/assets/f324b918-efba-4bc7-a592-32ed3d8dd692" />
).

**4. Failed-Then-Succeeded:** Identified brute-force payment gateway attacks by matching strings of `FAILED` transactions to a subsequent `SUCCESS` of the exact same amount.
![Pattern 4 Suspects](<img width="263" height="590" alt="Screenshot 2026-09-08 232252" src="https://github.com/user-attachments/assets/e7c76894-0eff-4150-bc5e-81e5a23bafc8" />
).

**5. Odd-Hour Concentration:** Detected automated bot scripts where over 80% of a user's transaction volume occurred between 2 AM and 5 AM.
![Pattern 5 Suspects](<img width="507" height="555" alt="Screenshot 2026-09-08 232458" src="https://github.com/user-attachments/assets/f9edb651-3fc0-4d7d-9026-08767dca1133" />
).

**Tier 2: Relational Logic**

**6. Mule Accounts:** Used correlated subqueries to track stolen funds entering an account and leaving within 30 minutes.
![Pattern 6 Suspects](<img width="273" height="468" alt="Screenshot 2026-09-08 232817" src="https://github.com/user-attachments/assets/179258ab-54ef-4e2e-95bb-f57fd3b823dc" />
).

**7. Refund Abuse:** Flagged accounts exploiting chargeback loopholes with refund rates exceeding 40%.
![Pattern 7 Suspects](<img width="502" height="469" alt="Screenshot 2026-09-08 232951" src="https://github.com/user-attachments/assets/9e6c8cbf-af0f-42fb-8834-badc4a2c90e3" />
).

**8. Merchant Collusion:** Built multi-step CTEs to identify money-laundering fronts where the top 5 customers accounted for over 60% of total merchant revenue.
![Pattern 8 Suspects](<img width="634" height="408" alt="Screenshot 2026-09-08 233144" src="https://github.com/user-attachments/assets/001496de-6caf-4e05-a1d1-3e0cb8a3c031" />
).

**9. Structuring (Smurfing):** Caught users deliberately keeping transactions at exactly ₹9,999 to evade Indian KYC regulatory thresholds.
![Pattern 9 Suspects](<img width="290" height="460" alt="Screenshot 2026-09-08 233301" src="https://github.com/user-attachments/assets/7ff4d254-8ac1-4e7e-b34c-1016db5db989" />
).

**10. Dormant-Then-Active (ATO):** Utilized the `LAG()` window function to identify Account Takeovers by finding 90+ day silent periods followed by sudden bursts of 15+ transactions.
![Pattern 10 Suspects](<img width="290" height="460" alt="Screenshot 2026-09-08 233301" src="https://github.com/user-attachments/assets/cefeaa78-93c2-4e90-99ed-bdbf5c7a7a5f" />
).

**Tier 3: Advanced Window Functions**

**11. Velocity Spikes:** Replaced standard averages with `UNBOUNDED PRECEDING` historical rolling averages to detect when a user's current monthly volume spiked to 5x their normal baseline.
![Pattern 11 Suspects](<img width="351" height="529" alt="Screenshot 2026-09-08 234955" src="https://github.com/user-attachments/assets/b772f26c-197f-4a60-b3cb-bf8209a80b80" />
).

**12. Geographic Impossibility:** Used `LAG()` to evaluate consecutive timestamps and locations, flagging accounts that changed cities faster than physically possible (under 60 minutes).
![Pattern 12 Suspects](<img width="260" height="440" alt="Screenshot 2026-09-08 235334" src="https://github.com/user-attachments/assets/7e7bf107-208e-444d-be68-2aaffc443527" />
)

## Repository Contents
*   `RedFlag_Nikunj.sql`: The complete analytical SQL script containing the logic for all detection patterns.
*   `screenshots/`: Visual evidence of successful query executions and suspect isolation.
*   *Note: The raw 18MB data file is excluded to simulate production security practices.*
