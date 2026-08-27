
# NYC Citi Bike Ridership Model

Analyzing NYC Citi Bike ridership patterns using bike trip data and weather information to understand factors that influence daily demand.

## Project Structure

### code/
Contains Jupyter notebooks used for analysis and modeling:
- `eda.ipynb` - Exploratory data analysis
- `preprocessing.ipynb` - Data cleaning and preparation
- `model.ipynb` - Predictive modeling (Part 2)

### data/
Contains exported datasets used for analysis, including the final CSV created from BigQuery.

### queries/
Contains SQL queries used to build and prepare the analysis dataset.

### docs/
Contains supporting documentation, notes, and project materials.

## Tools & Technologies

Python | SQL | BigQuery | Pandas | Scikit-learn | Jupyter Notebook

## Project Evidence

- Exploratory Data Analysis: `code/eda.ipynb`
- Data Preprocessing: `code/preprocessing.ipynb`
- Predictive Model: `code/model.ipynb`
- SQL Queries: `queries/`


## TLAB IV — Predicting Daily Citi Bike Ridership

For this project, I used the Citi Bike ridership and weather data from Part 1 to see if I could predict the number of rides on a given day. I started by exploring the data and looking for problems before building the model.

One of the issues I found was that there were 186 missing calendar dates between the first and last dates in the dataset. The missing dates were grouped into a few larger gaps instead of being spread out randomly. Since the final dataset was created with an INNER JOIN between the ride data and weather data, I believe the missing dates were most likely related to missing weather observations. I also found a precipitation value of 99.99, which was being used as a missing-value code. I changed that to a proper missing value during preprocessing. I also fixed the date and numeric data types and created the day-of-week variables needed for the model.

For the model, I used temperature, precipitation, wind speed, year, and day-of-week variables. I included year because the EDA showed that ridership increased over time as the Citi Bike system grew. I left out average trip duration because that information would not be available when trying to predict rides for the current day. I also did not use all three temperature columns because they are closely related.

The core Linear Regression model had a test R² of 0.7153. The MAE was 7,466.62 rides, meaning the predictions were typically off by about 7,467 rides. The RMSE was 9,243.70 rides, which was higher than the MAE because some days had larger prediction errors.

For my improvement, I added a squared temperature feature. I chose this because the EDA showed that ridership did not continue to increase in a perfectly straight line as the temperature got higher. Adding this feature improved the test R² from 0.7153 to 0.7281.

One weakness I noticed was that the residuals showed an upward trend over time. This suggests that the model was still underpredicting ridership more often in the later years. Weather and calendar information do not explain everything that affects bike usage. Having information about holidays, major events, station and bike availability, and membership growth could help make the predictions better.
