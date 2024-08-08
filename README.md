
https://public.tableau.com/views/Convoaiprojectdashboard/Dashboard2?:language=en-GB&:display_count=n&:origin=viz_share_link
Hi, I've created the following dashboard after preprocessing the data in the following steps i've appended below, do give it a read!

The data collection methodology employed in this project aims to provide a comprehensive analysis of Premier League team statistics over multiple seasons through web scraping on fbref.com.
https://docs.google.com/spreadsheets/d/1LFC22kRxI0MjjZdFPMQk_ZD03dULvEBMNJGo-iPxgyQ/edit?usp=sharing
above is the dataset link webscrapped and modified in the following steps
1. Iterating Over Seasons
The script dynamically iterates over specified seasons, ensuring flexibility in data collection across different timeframes. This allows for a comprehensive historical analysis of team performance.
Python

2. Fetching Standings Table and Team URLs
An initial HTTP request is made to the Premier League statistics page on fbref.com, and the BeautifulSoup library is utilized to parse the HTML content. The standings table is isolated, and team URLs are extracted for subsequent data retrieval.

3. Fetching Match and Shooting Data for Each Team
The script further drills down into individual team statistics. It iterates through each team URL, fetching detailed match data and extracting shooting statistics for a more nuanced understanding of team dynamics.

4. Merging Match and Shooting Data
To consolidate the obtained information, match and shooting data are merged based on the "Date" column. This step is crucial for creating a cohesive dataset for subsequent analysis.
5. Filtering Data for Premier League and Appending to Dataset
The collected data is meticulously filtered to include only Premier League matches, ensuring the integrity of the dataset. The information is then appended to the all_matches list, creating a comprehensive repository of team statistics.

PART 2: Data Preprocessing: Feature Engineering for Match Analysis
1. Day Code Assignment
To provide a numerical representation of the day of the week for each match, a new column named "day_code" has been introduced. This column assigns a specific code to each day, allowing for potential insights into whether certain teams perform differently on specific days.

2. Hour Extraction for Time Analysis
Aiming to explore potential correlations between match performance and the time of day, the "hour" column has been created. Extracting the hour from the "time" column and converting it into an integer facilitates a detailed examination of whether particular time slots influence team performance.
3. Opponent Encoding
In order to quantify opponent information, the "opp_code" column is introduced. Opponents are encoded as numerical values, providing a structured representation for further analysis of team performance against specific rivals.
4. Venue Encoding for Home Field Advantage
Recognizing the potential influence of the playing venue on team performance, the "venue_code" column has been created. This column encodes the venue information, with a specific focus on capturing the notion of home field advantage.


Part III: Data Preprocessing: Model Evaluation
1. Feature Selection:
The predictor variables for the model are chosen as ["venue_code", "opp_code", "hour", “day_code”
2. Model Evaluation:
The model is evaluated using accuracy_score and precision_score metrics on the test set.
3. Rolling Averages:
Rolling averages have been computed for key performance metrics, such as goals for (gf), goals against (ga), shots (sh), shots on target (sot), distance (dist), free kicks (fk), penalties (pk), and penalty attempts (pkatt). These rolling averages are applied to the data grouped by team, providing smoothed representations of team performance over time using a custom function 'rolling_averages'. The rolling window is set to 3 matches.
4. Model Training with Rolling Averages:
The RandomForestClassifier is re-trained using the original predictors along with the newly created rolling averages features.
