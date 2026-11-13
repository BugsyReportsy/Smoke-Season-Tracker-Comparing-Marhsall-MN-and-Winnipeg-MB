# Smoke-Season-Tracker-Comparing-Marhsall-MN-and-Winnipeg-MB
A comparative data pipeline analyzing wildfire-smoke conditions and weather in Marshall, Minnesota, and Winnipeg, Manitoba, from 2023 to 2026.
# Smoke Season Tracker: Marshall, MN vs. Winnipeg, MB

## Project Question

How many wildfire-smoke days did Marshall, Minnesota, and Winnipeg, Manitoba, experience during each summer from 2023 to 2026, and what weather conditions were associated with those days?

## Study Areas

### Marshall, Minnesota
- **City:** Marshall
- **State:** Minnesota, USA
- **Latitude:** 44.4469
- **Longitude:** -95.78835
- **Time Zone:** America/Chicago

### Winnipeg, Manitoba
- **City:** Winnipeg
- **Province:** Manitoba, Canada
- **Latitude:** 49.8844
- **Longitude:** -97.14704
- **Time Zone:** America/Winnipeg

**Study Period:** June 1 – September 30, 2023–2026

## Data Sources

- [Open-Meteo Geocoding API](https://open-meteo.com/en/docs/geocoding-api) – Obtaining city coordinates.
- [Open-Meteo Air Quality API](https://open-meteo.com/en/docs/air-quality-api) – Hourly PM2.5, US AQI, and aerosol optical depth measurements.
- [Open-Meteo Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api) – Historical precipitation, maximum temperature, wind speed, and wind direction.

## Data Pipeline

Extract → Transform → Combine → Load → Analyze

1. Extract hourly air-quality data for both cities from the Open-Meteo Air Quality API.
2. Extract historical weather data for the same locations and dates.
3. Convert hourly air-quality measurements into daily averages and maximums.
4. Handle missing values and verify that hourly measurements have consistent lengths.
5. Combine daily air-quality and weather data using the date.
6. Identify wildfire-smoke days using a PM2.5 threshold.
7. Load cleaned data into CSV and SQLite.
8. Analyze smoke-day frequency, seasonal patterns, and associated weather conditions.

## Smoke Day Definition

The primary smoke-day threshold is a daily mean PM2.5 concentration of **35.5 µg/m³ or higher**, corresponding to the beginning of the EPA's Unhealthy for Sensitive Groups category for 24-hour PM2.5.

Moderate smoke days are also identified when daily mean PM2.5 exceeds **9 µg/m³**.

Aerosol optical depth is used as additional supporting information when examining atmospheric haze.

## Key Findings

### Smoke Days by Summer

<img width="245" height="283" alt="Screenshot from 2026-11-12 20-14-16" src="https://github.com/user-attachments/assets/c9eb1819-65ff-4cc7-8bf3-1a4f1fc1d477" />



### Worst Smoke Days

<img width="662" height="346" alt="Screenshot from 2026-11-12 20-15-06" src="https://github.com/user-attachments/assets/6c842d5b-14b8-419b-a246-be410195d1c3" />


### Weather Conditions

<img width="785" height="84" alt="Screenshot from 2026-11-12 20-15-53" src="https://github.com/user-attachments/assets/86990d35-780d-439f-a7ff-da1fbf08c492" />


### City Comparison

Winnipeg was the city to have experienced the most smoke days, having faced a particularly high number of them during summer 2025.

## Charts

The project includes three visualizations:

1. Daily mean PM2.5 concentrations with the smoke-day threshold.
   <img width="1986" height="886" alt="daily_pm2_5" src="https://github.com/user-attachments/assets/0c854d63-b33b-4d5c-9302-e4e4b2b307bf" />

2. Smoke days per summer, comparing Marshall and Winnipeg.
   <img width="989" height="590" alt="highs_by_city_year" src="https://github.com/user-attachments/assets/7980bea4-3542-4626-b45c-558586904065" />

3. Hourly Heatmap for Worst Month
   <img width="1436" height="690" alt="worst_month_heatmap" src="https://github.com/user-attachments/assets/18440fb2-9dac-471f-b724-14f39eb0812d" />


![Daily PM2.5](charts/daily_pm25.png)

## Limitations

- Open-Meteo air-quality data is model-based rather than a direct measurement from an air-quality monitoring station in either city.
- The global air-quality dataset has an approximate spatial resolution of 45 km and a temporal resolution of three hours.
- Model estimates may not capture localized smoke concentrations or differences within each city.
- PM2.5 can originate from sources other than wildfires, including vehicles, industrial emissions, and other combustion sources.
- The selected PM2.5 threshold identifies elevated particulate pollution but cannot independently confirm that wildfire smoke caused it.
- Comparisons between cities should account for differences in geography, weather, and the location of the model grid cells.

## Reproducibility

The project was developed using Python in Google Colab.

**[Open Notebook in Google Colab](https://colab.research.google.com/drive/1EHcCY7mrrY74cxOchM0mXF6QMY4h_utV?usp=sharing)**

Libraries used:
- requests
- pandas
- matplotlib
- sqlite3
- json
- datetime

## Attribution

**Air Quality Data**

Air-quality data provided through [Open-Meteo](https://open-meteo.com/), using the [Open-Meteo Air Quality API](https://open-meteo.com/en/docs/air-quality-api).

The underlying atmospheric composition data is provided by the [Copernicus Atmosphere Monitoring Service (CAMS)](https://atmosphere.copernicus.eu/).

**Historical Weather Data**

Weather data provided by [Open-Meteo](https://open-meteo.com/), using the [Historical Weather API](https://open-meteo.com/en/docs/historical-weather-api).

**Geographic Coordinates**

City coordinates obtained using the [Open-Meteo Geocoding API](https://open-meteo.com/en/docs/geocoding-api).

Open-Meteo API data is provided under the [Creative Commons Attribution 4.0 International License (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

The data was retrieved, processed, aggregated, and combined for this project. These modifications should be considered when interpreting the resulting datasets and visualizations.

## Author

Don Huynh

## AI Use Note

I used ChatGPT to help understand the assignment, troubleshoot Python code, and organize parts of the data analysis. I ran the code in Google Colab and used the results from my own datasets to interpret the findings
