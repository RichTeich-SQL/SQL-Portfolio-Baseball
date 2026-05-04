Baseball Game Summary Analytics
Overview
This SQL script processes raw event logs from the tblEventLog2025 table to generate a comprehensive Game Summary Report. It pivots event-level data into team-level statistics, providing a side-by-side comparison of Visitor (VIS) and Home (HM) team performances for every game.
Key Metrics Captured
•	Standard Stats: At-Bats (AB), Hits, Home Runs (HRs), and total Runs.
•	Baserunning: Stolen Bases (SB) and Caught Stealing (CS) parsed via string patterns.
•	Clutch Hitting: RISP (Runners in Scoring Position) performance, including ABs, Hits, and a calculated Batting Average.
Logic Flow (CTEs)
The query uses a modular approach with three primary Common Table Expressions:
1.	GAMELIST: The initial aggregator. It identifies the home/away teams, extracts the date from the hteamdate string, and sums up hits, home runs, and baserunning events using CASE statements.
2.	RunScored: Specifically handles scoring logic. It checks the destination of the batter and all active runners (1st, 2nd, 3rd) to see if they crossed home plate (value > 3).
3.	GameStats: Joins the previous two CTEs to calculate final scores and determine the game winner.
Final Output Structure
The final result uses a UNION ALL to transform the data from a "Wide" format (one row per game) to a "Long" format (one row per team per game).
Column	Description
hteamdate	Unique game identifier.
dte	Formatted date (MM/DD).
team	The team abbreviation.
role	Indicates if the team was the Visitor (VIS) or Home (HM).
RISP_AVG	Calculated average with NULLIF to prevent divide-by-zero errors.

