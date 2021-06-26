# World_Weather_Analysis
Columbia Data Science Module 6

## Overview of Analysis

This project utilizes Openweather API to pull weather data for 2000 randomly generated coordinates. Using citipy, the nearest cities to these coordinates were collected. Following this, I used Google Maps API to pull the names of hotels near the selected cities. The end result for the user is the ability to specify the preferred weather for their next vacation and after this they are provided a map of hotels that meet their specifications. Using the Google maps API, I also created an itinerary for a hypethetical trip between four cities in Australia. 

## Resources
Software: Python 3.8.6, Jupyter Notebook

Python packages: citipy, gmaps, requests, pandas, matplotlib, numpy, datetime

APIs: OpenWeatherMap, Google Maps

## Building the App

### Creating the Weather Database

The first step in creating the app was pulling weather data. To start, I randomly generated 1500 pairs of longitudinal and latitudinal coordinates using the code below: 

![coordinate_generation.PNG](Resources/coordinate_generation.PNG) 

Next, using citipy, I retrieved the nearest city to each coordinate. Some random coordinates were in uninhabited areas like the ocean or Antarctica. Additionally, I specified that only unique cities should be added to the list of cities. 

![citipy.PNG](Resources/citipy.PNG) 

This left 630 cities in the cities list. The OpenWeather API was then used to pull the weather for each of the cities in that list using the code below: 

![openweather_api.PNG](Resources/openweather_api.PNG) 

After converting the data to a data frame and reordering the columns, we are left with this: 

![weather_df.PNG](Resources/weather_df.PNG) 

I then exported the data frame as [WeatherPy_Database.csv](https://github.com/perryabdulkadir/World_Weather_Analysis/blob/main/Weather_Database/WeatherPy_Database.csv) and saved it to the Weather_Database folder.

### Creating a Customer Travel Destinations Map

After loading the WeatherPy_Database.csv into the Vacation_Search.ipynb, I wrote code prompting users to select their minimum and maximum preferred temperatures. 

```
min_temp = float(input("What is the minimum temperature you would like for your trip? "))
max_temp = float(input("What is the maximum temperature you would like for your trip? "))
```

Next, I used the loc method the filter the data frame based on the user's inputs. 

![loc_filter.PNG](Resources/loc_filter.PNG) 

Then, I created a clean version of the data frame by dropping empty rows.
```
clean_df = preferred_cities_df[preferred_cities_df['Country'].notna()]
```

After preparing clean_df, I created a data frame identical to clean_df but with an empty column called "Hotel Name." This new dataframe is called hotel_df.

```
# 5a. Create DataFrame called hotel_df to store hotel names along with city, country, max temp, and coordinates.
hotel_df = clean_df[["City", "Country", "Max Temp", "Description", "Lat", "Lng"]].copy()

# 5b. Create a new column "Hotel Name"
hotel_df["Hotel Name"] = ""
```


## Summary



-----

### **Contact:**

**Email:** perry.abdulkadir@alumni.harvard.edu

**Linkedin:** https://www.linkedin.com/in/perry-abdulkadir-6a255199/
