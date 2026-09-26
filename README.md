🏏 IPL Analysis (2008 - 2025) - Power BI Dashboard

Welcome to the IPL Analysis (2008-2025) repository. This project is a comprehensive data analysis and visual dashboard built using Microsoft Power BI. It transforms multi-season IPL match datasets into actionable, interactive cricket analytics—tracking seasonal champions, individual player performances (Orange & Purple Cap holders), team standings, and boundary metrics.

📌 Table of Contents

Project Overview

Key Features

Data Architecture & Modeling

DAX Calculations

Challenges & Solutions

How to View the Report

Technologies Used

🏏 Project Overview

Data in its raw form can be overwhelming. By leveraging Power BI, this project cleans, structures, and visualizes over a decade of Indian Premier League (IPL) data. It allows cricket enthusiasts and analysts to filter by season and observe changing team dynamics, player consistency, and overall league statistics.

Dashboard Highlights:

Season-Level Filtering: Dynamic slice enabling view toggles across all IPL seasons.

KPI Metrics Cards: Instant tracking of total boundaries (4s and 6s), total matches, venues, centuries, and half-centuries.

Top Performers (Cap Holders): Dynamic display of Orange Cap (Most Runs) and Purple Cap (Most Wickets) leaders per season.

Points Table: Automated points calculation displaying matches played, won, lost, tied, no result, and overall points alongside team logos.

Interactive Navigation: Side panel integration with external web links (e.g., Cricinfo, Cricbuzz, official IPL handles).

🏗 Data Architecture & Modeling

The project employs a structured data model connecting several core tables to enable efficient multi-dimensional analysis.

Data Tables:

ball_by_ball_data: Contains ball-level detail including runs, wickets, extras, batter, bowler, and over numbers.

ipl_matches_data: Contains high-level match metadata including match ID, date, venue, season, winner, and match type.

players-data-updated: Includes player profile details, batting style, bowling style, and image links.

teams_data: Contains team metadata, team IDs, short names, and image URLs for team logos.

Relationships:

ipl_matches_data $\leftrightarrow$ ball_by_ball_data: One-to-Many ($1 : *$) relationship linked by match_id.

players-data-updated $\leftrightarrow$ ipl_matches_data / ball_by_ball_data: One-to-Many relationships for player attribute lookups.

teams_data $\leftrightarrow$ ipl_matches_data: One-to-Many relationships mapped for team stats and logo displays.

🧮 DAX Calculations

Custom Data Analysis Expressions (DAX) were authored to handle dynamic dynamic filtering and ranking across seasons.

Example: Orange Cap Holder Calculation

Orange Cap Holder = 

VAR SelectedSeason = SELECTEDVALUE(ipl_matches_data[season])

VAR SeasonDataOnly = 
    FILTER(ball_by_ball_data, RELATED(ipl_matches_data[season]) = SelectedSeason)

VAR RunSummary = 
    SUMMARIZE(SeasonDataOnly, ball_by_ball_data[batter], "Total Runs", SUM(ball_by_ball_data[batter_runs]))

VAR MaxRuns = MAXX(RunSummary, [Total Runs])

VAR TopScorer = 
    CALCULATETABLE(VALUES(ball_by_ball_data[batter]), FILTER(RunSummary, [Total Runs] = MaxRuns))

RETURN MAXX(TopScorer, ball_by_ball_data[batter])


💡 Challenges & Solutions

Dynamic Image Rendering (Team & Player Logos):

Challenge: Rendering external web images/logos dynamically inside tables and KPI cards initially caused missing visual components or raw URL texts.

Solution: Standardized image URLs, set the Data Category to Image URL within the Data View properties, and properly configured the Image visual containers within Power BI.

🚀 How to View the Report

Clone or download this repository to your local machine:

git clone https://github.com/your-username/ipl-analysis-powerbi.git


Download and install Microsoft Power BI Desktop.

Open the .pbix file included in the repository.

Interact with the filters, slicers, and navigation buttons.

🛠 Technologies Used

Business Intelligence: Microsoft Power BI

Data Transformation: Power Query (ETL process, duplicate removal, schema layout)

Calculations: DAX (Data Analysis Expressions)

Data Source: IPL Ball-by-Ball & Match Datasets (2008–2025)

💬 Author & Feedback

Created with 🏏 passion for cricket and data analytics. If you have any suggestions or feedback, feel free to connect or open an issue!
