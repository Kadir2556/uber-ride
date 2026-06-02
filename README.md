An Exploratory Data Analysis (EDA) project focused on cleaning, processing, and analyzing Uber trip data. This project extracts key operational insights such as passenger distribution, fare trends, and peak demand hours using Python data science libraries.

##  Features & Analysis Scope
- *Data Cleaning:* Handling missing values, checking data types, and stripping unnecessary formatting.
- *Fare vs. Passenger Volume:* Analyzing how total fare amounts correlate with the number of passengers per ride.
- *Time-Series Insights:* Extracting hour-of-day variables to isolate and highlight peak booking hours.
- *Data Visualizations:* Generating heatmaps, box plots, and bar charts to present actionable trends visually.

## Tech Stack & Dependencies
This project is built using Python and the following core libraries:
* *Pandas* - For data manipulation, filtering, and aggregation.
* *NumPy* - For handling numerical arrays and structural data.
* *Matplotlib* - For basic plot configurations and charting structure.
* *Seaborn* - For generating advanced visualizations like heatmaps and distribution plots.

## Key Insights Found
- *Top Busy Hours:* The dataset identifies clear operational peak windows throughout the day (tracked via value counts on the booking hours).
- *Fare Trends:* Boxplots reveal the variance and outliers in fare distribution relative to standard passenger counts.
- *Feature Correlations:* The correlation matrix highlights dependencies between fare amounts, trip timing, and passenger clusters.
