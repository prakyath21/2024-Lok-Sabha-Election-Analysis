# 2024-Lok-Sabha-Election-Analysis
---

# India General Elections 2024 - SQL Analysis

This project analyzes the 2024 India General Election results using SQL queries to explore data on seats won by alliances, candidate statistics, and vote breakdowns by state.

## Project Overview

This analysis includes:
- Total seats won by each alliance (`NDA`, `I.N.D.I.A`, and `OTHER`)
- Breakdown of votes by EVM and postal
- Party-wise and candidate-wise seat counts per state
- Determination of winning and runner-up candidates for each constituency

## Database Schema

The following tables are used:
1. `constituencywise_results`: Stores results by constituency
2. `statewise_results`: State-wise aggregation of results
3. `partywise_results`: Details by political party
4. `constituencywise_details`: Detailed voting breakdown by candidate

---

## Schema/ERD Diagram
![Alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/Entity%20relationship.png?raw=true)


## SQL Queries

### 1. Total Seats
Counts the total number of seats in the election.

```sql
SELECT DISTINCT COUNT(Parliament_Constituency) AS Total_Seats
FROM constituencywise_results;
```


### 2.Calculates total seats available in each state.
``` sql
SELECT s.State AS State_Name, COUNT(cr.Constituency_ID) AS Total_Seats_Available
FROM constituencywise_results cr
JOIN statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN states s ON sr.State_ID = s.State_ID
GROUP BY s.State
ORDER BY s.State;
```
### 
