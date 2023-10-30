# Python API Challenge: WeatherPy & VacationPy

### Overview
The primary objective of this project is to answer the question: "What is the weather like as we approach the equator?" Using Python requests, APIs, and JSON traversals, we aim to provide a comprehensive answer to this question.

### Comparative Weather Analysis Across Latitudes

<div align="center">
    <img src="https://github.com/Xthe23/python-api-challenge/blob/main/Resources/Fig1.png" width="300">
    <img src="https://github.com/Xthe23/python-api-challenge/blob/main/Resources/Fig2.png" width="300">
    <img src="https://github.com/Xthe23/python-api-challenge/blob/main/Resources/Fig3.png" width="300">
    <img src="https://github.com/Xthe23/python-api-challenge/blob/main/Resources/Fig4.png" width="300">
</div>

# Part 1: WeatherPy
In this section, we analyze the weather of over 500 cities with varying distances from the equator using the citipy library and the OpenWeatherMap API.

Below is a snippet of the `WeatherPy.ipynb` file used in this project. 
For the complete code, please [click here](https://github.com/Xthe23/python-api-challenge/blob/main/WeatherPy.ipynb).

```python
# Run an API request for each of the cities
    try:
        # Parse the JSON and retrieve data
        city_weather = requests.get(city_url).json()

        # Parse out latitude, longitude, max temp, humidity, cloudiness, wind speed, country, and date
        city_lat = city_weather["coord"]["lat"]
        city_lng = city_weather["coord"]["lon"]
        city_max_temp = city_weather["main"]["temp_max"]
        city_humidity = city_weather["main"]["humidity"]
        city_clouds = city_weather["clouds"]["all"]
        city_wind = city_weather["wind"]["speed"]
        city_country = city_weather["sys"]["country"]
        city_date = city_weather["dt"]

        # Append the City information into city_data list
        city_data.append({"City": city, 
                          "Lat": city_lat, 
                          "Lng": city_lng, 
                          "Max Temp": city_max_temp,
                          "Humidity": city_humidity,
                          "Cloudiness": city_clouds,
                          "Wind Speed": city_wind,
                          "Country": city_country,
                          "Date": city_date})

    # If an error is experienced, skip the city
    except:
        print("City not found. Skipping...")
        pass
```

### Key Features:
- Scatter plots showcasing relationships between:
- Latitude vs. Temperature
- Latitude vs. Humidity
- Latitude vs. Cloudiness
- Latitude vs. Wind Speed
- Linear regression plots for the Northern and Southern Hemispheres for each of the above relationships.

# Part 2: VacationPy
In this section, we use the weather data to plan future vacations using the geoViews library and the Geoapify API.

Below is a snippet of the `VacationPy.ipynb` file used in this project. 
For the complete code, please [click here](https://github.com/Xthe23/python-api-challenge/blob/main/VacationPy.ipynb).

```python
# Set parameters to search for a hotel
radius = 10000 # meters
limit = 1

params = {
    "radius": radius,
    "type": "accommodation.hotel",
    "apiKey": geoapify_key
}

# Print a message to follow up the hotel search
print("Starting hotel search")

# Iterate through the hotel_df DataFrame
for index, row in hotel_df.iterrows():
    # get latitude, longitude from the DataFrame
    lat = row["Lat"]
    lng = row["Lng"]
    
    # Add filter and bias parameters with the current city's latitude and longitude to the params dictionary
    params["filter"] = f"circle:{lng},{lat},{radius}"
    params["bias"] = f"proximity:{lng},{lat}"
    
    # Set base URL
    base_url = "https://api.geoapify.com/v2/places"


    # Make and API request using the params dictionary
    name_address = requests.get(base_url, params=params).json()
    # Convert the API response to JSON format
    
    
    # Grab the first hotel from the results and store the name in the hotel_df DataFrame
    try:
        hotel_df.loc[index, "Hotel Name"] = name_address["features"][0]["properties"]["name"]
    except (KeyError, IndexError):
        # If no hotel is found, set the hotel name as "No hotel found".
        hotel_df.loc[index, "Hotel Name"] = "No hotel found"
        
    # Log the search results
    print(f"{hotel_df.loc[index, 'City']} - nearest hotel: {hotel_df.loc[index, 'Hotel Name']}")
```

### Key Features:
- Map displaying a point for every city based on humidity.
- Identification of cities with ideal weather conditions.
- Map showcasing hotels within 10,000 meters of the identified cities.

# Acknowledgements

[OpenWeatherMap API](https://openweathermap.org/api)

[Geoapify API](https://www.geoapify.com/)

[citipy Python library](https://pypi.org/project/citipy/)
