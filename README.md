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

Key Features:
Scatter plots showcasing relationships between:
Latitude vs. Temperature
Latitude vs. Humidity
Latitude vs. Cloudiness
Latitude vs. Wind Speed
Linear regression plots for the Northern and Southern Hemispheres for each of the above relationships.

# Part 2: VacationPy
In this section, we use the weather data to plan future vacations using the geoViews library and the Geoapify API.

### Key Features:
- Map displaying a point for every city based on humidity.
- Identification of cities with ideal weather conditions.
- Map showcasing hotels within 10,000 meters of the identified cities.

# Acknowledgements

[OpenWeatherMap API](https://openweathermap.org/api)

[Geoapify API](https://www.geoapify.com/)

[citipy Python library](https://pypi.org/project/citipy/)
