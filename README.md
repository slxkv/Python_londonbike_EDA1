# City Bike Ride
## EDA & Data Visualisation for bike sharing in London

Bike-sharing systems are getting popular especially among big cities around the world. The system helps to promote eco-friendly mode of travel by lowering carbon emission, reduce traffic congestion, and encourage healthy lifestyles. 

This project was created out of a desire to navigate and understand how the trend of bike-sharing system in London throughout the period from 2015 to 2017. It delves into the count of bike share over the year and how a few variables that might affect the total count. All of this to help businesses optimize operations, improve customer experiences, and make strategic decisions.

### Key pain point?
One of the departments want to know the trend of bike ride share in London over the span of 3 years from 2015-2017. 
This is mainly to;
- improve inventory management by having the right number of bikes at the right time, reducing operational costs. 
- Implement predictive maintenance on bikes, scheduling repairs and checks during low-demand periods.
- Wether company should partner with local businesses to offer services like waterproof covers or gear rentals on different weather conditions.


### Data Source
The data sourced from Kaggle Dataset: London bike sharing dataset
by Hristo Mavrodiev which provides a foundation for my analysis, containing detailed information on count of bike share, timestamp, temperature, season, windspeed, and humidity. 


## The Question
Through a series of Python scripts, I explore a few key questions that I want to answer in this project.

1. How the season changes impact the sum of bike share 
2. Does the weather gives effect on the sum of bike share
3. Correlation between temperature and windspeed 
4. How the bike ride share change over time
4. What is the peak bussiness hour?


# Data Preparation and Cleanup

```python
# Importing Libraries
import ast
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt  
import zipfile
import kaggle

# download dataset from kaggle using the Kaggle API
!kaggle datasets download -d hmavrodiev/london-bike-sharing-dataset

# extract the file from the downloaded zip file
zipfile_name = 'london-bike-sharing-dataset.zip'
with zipfile.ZipFile(zipfile_name, 'r') as file:
    file.extractall()

# read in the csv file as a pandas dataframe
bikes = pd.read_csv("london_merged.csv")
```

## Important Metadata

- "timestamp" - timestamp field for grouping the data
- "cnt" - the count of a new bike shares
- "t1" - real temperature in C
- "t2" - temperature in C "feels like"
- "hum" - humidity in percentage
- "windspeed" - wind speed in km/h
- "weathercode" - category of the weather
- "isholiday" - boolean field - 1 holiday / 0 non holiday
- "isweekend" - boolean field - 1 if the day is weekend
- "season" - category field meteorological seasons: 
    - -- 0-spring ; 1-summer; 2-fall; 3-winter.
- "weather_code" category description:

    - -- 1 = Clear ; mostly clear but have some values with haze/fog/patches of fog/ fog in vicinity 
    - -- 2 = scattered clouds / few clouds 
    - -- 3 = Broken clouds 
    - -- 4 = Cloudy 
    - -- 7 = Rain/ light Rain shower
    - -- 10 = rain with thunderstorm 
    - -- 26 = snowfall 
    - -- 94 = Freezing Fog

## Data exploration notes

This is where the data inspection were done, wheter there's an errors, inconcsistencies, bugs, weird or any corrupted characters etc that should be corrected.

1. Make sure there's no null or NaN value, replace it with significant value if possible.
2. Two temperature columns were seen, need to decide which one is more valueble to be included into the analysis part.
3. From Metadata notes above, we cna detect that weather_code and season columns are numerical value but can be specified as categorical variables
4. The is_holiday and is_weekend columns are  boolean variables
5. Besides timestamp which obviously a date-time object, we can make numerical analysis on the rest of the columns

## Data Cleaning 

The aim is to refine our dataset to ensure it is structured and ready for analysis.

- Only relevant columns should be retained.
- T2 column is dropped as the correlation between T2 and T1 is high
- Season and weather dictionary were created, as to map the integers value to actual and meaningful value.
- Changed the timestamp column datatype, from object to datetime type and make the timestamp as index for easier analysis.
- New column was made for each year, month and day extracted from timestamp column.

View my notebook for detailed steps here:
[london_bike1.ipynb](london_bike1.ipynb)

# The Analysis

## 1. Distribution of Total Bike Rides by Season

![Pie Chart for Sum of Bike Share each Season](Visualisation_images\season_1.png)

### Insight 

- Summer: Accounts for the highest proportion of bike rides at 32.3%.
- Autumn: Represents 25.5% of total bike rides.
- Spring: Comprises 24.4% of the rides, close to autumn.
- Winter: Has the lowest share of bike rides at 17.9%.
This indicates that bike rides are most popular in the summer and least popular in the winter.

