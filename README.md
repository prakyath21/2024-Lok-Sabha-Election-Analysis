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
![Alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/Total%20Seats.png?raw=true)


### 2.Calculates total seats available in each state.
``` sql
SELECT s.State AS State_Name, COUNT(cr.Constituency_ID) AS Total_Seats_Available
FROM constituencywise_results cr
JOIN statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN states s ON sr.State_ID = s.State_ID
GROUP BY s.State
ORDER BY s.State;
```
![Alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/Seats_for_each_state.png?raw=true)

### 3.Total Seats Won by NDA Allianz 
``` sql
SELECT 
    SUM(CASE 
            WHEN party IN (
                'Bharatiya Janata Party - BJP', 
                'Telugu Desam - TDP', 
				'Janata Dal  (United) - JD(U)',
                'Shiv Sena - SHS', 
                'AJSU Party - AJSUP', 
                'Apna Dal (Soneylal) - ADAL', 
                'Asom Gana Parishad - AGP',
                'Hindustani Awam Morcha (Secular) - HAMS', 
                'Janasena Party - JnP', 
				'Janata Dal  (Secular) - JD(S)',
                'Lok Janshakti Party(Ram Vilas) - LJPRV', 
                'Nationalist Congress Party - NCP',
                'Rashtriya Lok Dal - RLD', 
                'Sikkim Krantikari Morcha - SKM'
            ) THEN [Won]
            ELSE 0 
        END) AS NDA_Total_Seats_Won
FROM 
    partywise_results

```
![Alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/NDA_TOTAL_SEATS.png?raw=true)

### 4.Total Seats Won by NDA Allianz Parties.
``` sql
SELECT 
    party as Party_Name,
    won as Seats_Won
FROM 
    partywise_results
WHERE 
    party IN (
        'Bharatiya Janata Party - BJP', 
        'Telugu Desam - TDP', 
		'Janata Dal  (United) - JD(U)',
        'Shiv Sena - SHS', 
        'AJSU Party - AJSUP', 
        'Apna Dal (Soneylal) - ADAL', 
        'Asom Gana Parishad - AGP',
        'Hindustani Awam Morcha (Secular) - HAMS', 
        'Janasena Party - JnP', 
		'Janata Dal  (Secular) - JD(S)',
        'Lok Janshakti Party(Ram Vilas) - LJPRV', 
        'Nationalist Congress Party - NCP',
        'Rashtriya Lok Dal - RLD', 
        'Sikkim Krantikari Morcha - SKM'
    )
ORDER BY Seats_Won DESC
```
![Alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/NDA_TOTAL_SEATS_PARTIES.png?raw=true)

### 5.Total Seats won by I.N.D.I.A.

``` sql
SELECT 
    SUM(CASE 
            WHEN party IN (
                'Indian National Congress - INC',
                'Aam Aadmi Party - AAAP',
                'All India Trinamool Congress - AITC',
                'Bharat Adivasi Party - BHRTADVSIP',
                'Communist Party of India  (Marxist) - CPI(M)',
                'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
                'Communist Party of India - CPI',
                'Dravida Munnetra Kazhagam - DMK',
                'Indian Union Muslim League - IUML',
                'Nat`Jammu & Kashmir National Conference - JKN',
                'Jharkhand Mukti Morcha - JMM',
                'Jammu & Kashmir National Conference - JKN',
                'Kerala Congress - KEC',
                'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
                'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
                'Rashtriya Janata Dal - RJD',
                'Rashtriya Loktantrik Party - RLTP',
                'Revolutionary Socialist Party - RSP',
                'Samajwadi Party - SP',
                'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
                'Viduthalai Chiruthaigal Katchi - VCK'
            ) THEN [Won]
            ELSE 0 
        END) AS INDIA_Total_Seats_Won
FROM 
    partywise_results
```
![Alt Text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/INDIA_TOTAL_SEATS_WON.png?raw=true)

### 6.Seats Won by I.N.D.I.A. Allianz Parties
``` sql
SELECT 
    party as Party_Name,
    won as Seats_Won
FROM 
    partywise_results
WHERE 
    party IN (
        'Indian National Congress - INC',
                'Aam Aadmi Party - AAAP',
                'All India Trinamool Congress - AITC',
                'Bharat Adivasi Party - BHRTADVSIP',
                'Communist Party of India  (Marxist) - CPI(M)',
                'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
                'Communist Party of India - CPI',
                'Dravida Munnetra Kazhagam - DMK',
                'Indian Union Muslim League - IUML',
                'Nat`Jammu & Kashmir National Conference - JKN',
                'Jharkhand Mukti Morcha - JMM',
                'Jammu & Kashmir National Conference - JKN',
                'Kerala Congress - KEC',
                'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
                'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
                'Rashtriya Janata Dal - RJD',
                'Rashtriya Loktantrik Party - RLTP',
                'Revolutionary Socialist Party - RSP',
                'Samajwadi Party - SP',
                'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
                'Viduthalai Chiruthaigal Katchi - VCK'
    )
ORDER BY Seats_Won DESC
```
![Alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/INDIA_TOTAL_SEATS_WON_PARTIES.png?raw=true)

### 7.Adding new column field in table partywise_results to get the Party Allianz as NDA, I.N.D.I.A and OTHER.
``` sql
ALTER TABLE partywise_results
ADD party_alliance VARCHAR(50);
I.N.D.I.A Allianz
UPDATE partywise_results
SET party_alliance = 'I.N.D.I.A'
WHERE party IN (
    'Indian National Congress - INC',
    'Aam Aadmi Party - AAAP',
    'All India Trinamool Congress - AITC',
    'Bharat Adivasi Party - BHRTADVSIP',
    'Communist Party of India  (Marxist) - CPI(M)',
    'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
    'Communist Party of India - CPI',
    'Dravida Munnetra Kazhagam - DMK',	
    'Indian Union Muslim League - IUML',
    'Jammu & Kashmir National Conference - JKN',
    'Jharkhand Mukti Morcha - JMM',
    'Kerala Congress - KEC',
    'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
    'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
    'Rashtriya Janata Dal - RJD',
    'Rashtriya Loktantrik Party - RLTP',
    'Revolutionary Socialist Party - RSP',
    'Samajwadi Party - SP',
    'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
    'Viduthalai Chiruthaigal Katchi - VCK'
);
NDA Allianz
UPDATE partywise_results
SET party_alliance = 'NDA'
WHERE party IN (
    'Bharatiya Janata Party - BJP',
    'Telugu Desam - TDP',
    'Janata Dal  (United) - JD(U)',
    'Shiv Sena - SHS',
    'AJSU Party - AJSUP',
    'Apna Dal (Soneylal) - ADAL',
    'Asom Gana Parishad - AGP',
    'Hindustani Awam Morcha (Secular) - HAMS',
    'Janasena Party - JnP',
    'Janata Dal  (Secular) - JD(S)',
    'Lok Janshakti Party(Ram Vilas) - LJPRV',
    'Nationalist Congress Party - NCP',
    'Rashtriya Lok Dal - RLD',
    'Sikkim Krantikari Morcha - SKM'
);
OTHER
UPDATE partywise_results
SET party_alliance = 'OTHER'
WHERE party_alliance IS NULL;
```
### 8.Which party alliance (NDA, I.N.D.I.A, or OTHER) won the most seats across all states?
``` sql
SELECT 
    p.party_alliance,
    COUNT(cr.Constituency_ID) AS Seats_Won
FROM 
    constituencywise_results cr
JOIN 
    partywise_results p ON cr.Party_ID = p.Party_ID
WHERE 
    p.party_alliance IN ('NDA', 'I.N.D.I.A', 'OTHER')
GROUP BY 
    p.party_alliance
ORDER BY 
    Seats_Won DESC;
```
![Alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/MOST_SEATS_WON.png?raw=true)

### 9.Winning candidate's name, their party name, total votes, and the margin of victory for a specific state and constituency?

```sql
SELECT cr.Winning_Candidate, p.Party, p.party_alliance, cr.Total_Votes, cr.Margin, cr.Constituency_Name, s.State
FROM constituencywise_results cr
JOIN partywise_results p ON cr.Party_ID = p.Party_ID
JOIN statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN states s ON sr.State_ID = s.State_ID
WHERE s.State = 'Uttar Pradesh' AND cr.Constituency_Name = 'AMETHI';
```
![Alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/Winning_candidate_particular_state.png?raw=true)

### 10.Distribution of EVM votes versus postal votes for candidates in a specific constituency?
```sql
SELECT 
    cd.Candidate,
    cd.Party,
    cd.EVM_Votes,
    cd.Postal_Votes,
    cd.Total_Votes,
    cr.Constituency_Name
FROM 
    constituencywise_details cd
JOIN 
    constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
WHERE 
    cr.Constituency_Name = 'MATHURA'
ORDER BY cd.Total_Votes DESC;
```
![Alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/EVM_VOTES_VS_POSTAL_VOTES.png?raw=true)

### 11. Which parties won the most seats in s State, and how many seats did each party win?
``` sql
SELECT 
    p.Party,
    COUNT(cr.Constituency_ID) AS Seats_Won
FROM 
    constituencywise_results cr
JOIN 
    partywise_results p ON cr.Party_ID = p.Party_ID
JOIN 
    statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN states s ON sr.State_ID = s.State_ID
WHERE 
    s.state = 'Andhra Pradesh'
GROUP BY 
    p.Party
ORDER BY 
    Seats_Won DESC;
```
![alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/PARTY_WON_MOST_SEATS_STATES.png?raw=true)

### 12. What is the total number of seats won by each party alliance (NDA, I.N.D.I.A, and OTHER) in each state for the India Elections 2024.
``` sql
SELECT 
    s.State AS State_Name,
    SUM(CASE WHEN p.party_alliance = 'NDA' THEN 1 ELSE 0 END) AS NDA_Seats_Won,
    SUM(CASE WHEN p.party_alliance = 'I.N.D.I.A' THEN 1 ELSE 0 END) AS INDIA_Seats_Won,
	SUM(CASE WHEN p.party_alliance = 'OTHER' THEN 1 ELSE 0 END) AS OTHER_Seats_Won
FROM 
    constituencywise_results cr
JOIN 
    partywise_results p ON cr.Party_ID = p.Party_ID
JOIN 
    statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN 
    states s ON sr.State_ID = s.State_ID
WHERE 
    p.party_alliance IN ('NDA', 'I.N.D.I.A',  'OTHER')  -- Filter for NDA and INDIA alliances
GROUP BY 
    s.State
ORDER BY 
    s.State;

```
![alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/TOTAL_SEATS_EACH_ALLIANCE.png?raw=true)

### 13. Which candidate received the highest number of EVM votes in each constituency (Top 10)?
``` sql
SELECT TOP 10
    cr.Constituency_Name,
    cd.Constituency_ID,
    cd.Candidate,
    cd.EVM_Votes
FROM 
    constituencywise_details cd
JOIN 
    constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
WHERE 
    cd.EVM_Votes = (
        SELECT MAX(cd1.EVM_Votes)
        FROM constituencywise_details cd1
        WHERE cd1.Constituency_ID = cd.Constituency_ID
    )
ORDER BY 
    cd.EVM_Votes DESC;
```
![ALT TEXT](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/HIGHES_CANDIDATE.png?raw=true)

### 14.Which candidate won and which candidate was the runner-up in each constituency of State for the 2024 elections?
``` SQL
WITH RankedCandidates AS (
    SELECT 
        cd.Constituency_ID,
        cd.Candidate,
        cd.Party,
        cd.EVM_Votes,
        cd.Postal_Votes,
        cd.EVM_Votes + cd.Postal_Votes AS Total_Votes,
        ROW_NUMBER() OVER (PARTITION BY cd.Constituency_ID ORDER BY cd.EVM_Votes + cd.Postal_Votes DESC) AS VoteRank
    FROM 
        constituencywise_details cd
    JOIN 
        constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
    JOIN 
        statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
    JOIN 
        states s ON sr.State_ID = s.State_ID
    WHERE 
        s.State = 'Maharashtra'
)

SELECT 
    cr.Constituency_Name,
    MAX(CASE WHEN rc.VoteRank = 1 THEN rc.Candidate END) AS Winning_Candidate,
    MAX(CASE WHEN rc.VoteRank = 2 THEN rc.Candidate END) AS Runnerup_Candidate
FROM 
    RankedCandidates rc
JOIN 
    constituencywise_results cr ON rc.Constituency_ID = cr.Constituency_ID
GROUP BY 
    cr.Constituency_Name
ORDER BY 
    cr.Constituency_Name;

```
![alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/RUNNER_UP.png?raw=true)
![ALT TEXT](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/RUNNER_UP_2.png?raw=true)

### 15.For the state of 'Telangana', what are the total number of seats, total number of candidates, total number of parties, total votes (including EVM and postal), and the breakdown of EVM and postal votes?
``` sql
SELECT 
    COUNT(DISTINCT cr.Constituency_ID) AS Total_Seats,
    COUNT(DISTINCT cd.Candidate) AS Total_Candidates,
    COUNT(DISTINCT p.Party) AS Total_Parties,
    SUM(cd.EVM_Votes + cd.Postal_Votes) AS Total_Votes,
    SUM(cd.EVM_Votes) AS Total_EVM_Votes,
    SUM(cd.Postal_Votes) AS Total_Postal_Votes
FROM 
    constituencywise_results cr
JOIN 
    constituencywise_details cd ON cr.Constituency_ID = cd.Constituency_ID
JOIN 
    statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
JOIN 
    states s ON sr.State_ID = s.State_ID
JOIN 
    partywise_results p ON cr.Party_ID = p.Party_ID
WHERE 
    s.State = 'Telangana';
```
![alt text](https://github.com/prakyath21/2024-Lok-Sabha-Election-Analysis/blob/main/images/Total_seats_telangana.png?raw=true)



