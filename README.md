# City Bike Ride
## EDA & Data Visualisation for bike sharing in London

Bike-sharing systems are getting popular especially among big cities around the world. The system helps to promote eco-friendly mode of travel by lowering carbon emission, reduce traffic congestion, and encourage healthy lifestyles. 

This project was created out of a desire to navigate and understand how the trend of bike-sharing system in London throughout the period from 2015 to 2017. It delves into the count of bike share over the year and how a few variables that might affect the total count. All of this to help businesses optimize operations, improve customer experiences, and make strategic decisions.

The data sourced from Kaggle Dataset: London bike sharing dataset
by Hristo Mavrodiev which provides a foundation for my analysis, containing detailed information on count of bike share, timestamp, temperature, season, windspeed, and humidity. 

Through a series of Python scripts, I explore a few key questions that I want to answer in this project.

## The Question

1. How the season changes impact the sum of bike share 
2. Does the weather gives effect on the sum of bike share
3. Correlation between temperature and windspeed 
4. How the bike ride share change over time
4. What is the peak bussiness hour?

## Data Preparation and Cleanup

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

