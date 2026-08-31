# Weather ETL Pipeline

A simple ETL (Extract, Transform, Load) pipeline built in Python that pulls live weather data from the OpenWeather API for multiple cities, cleans and structures it with Pandas, and stores it as a CSV for analysis.

Built as part of Week 7 of the AnalystLab Africa Data Analytics Internship (#AnalystLabAfrica).

---

## Project Overview

Data analysts regularly work with data pulled from external APIs. This project demonstrates a complete, minimal ETL workflow: extracting real-time weather data via API, transforming it into a clean tabular format, loading it into a CSV file, and performing basic comparative analysis across cities.

## Data Source

- **[OpenWeather API](https://openweathermap.org/api)** — Current Weather Data endpoint
- Free tier account, personal API key required
- Data pulled for: **Nairobi, London, New York**

## Tools Used

- Python
- `requests` — API calls
- `pandas` — data structuring and transformation
- `python-dotenv` — securely loading the API key from a `.env` file
- Jupyter Notebook

## ETL Process

### 1. Extract
- Connected to the OpenWeather `/data/2.5/weather` endpoint using a securely stored API key (loaded via `.env`, excluded from GitHub via `.gitignore`).
- Looped through 3 cities, retrieving live weather data for each.
- Extracted key fields from each nested API response: city name, temperature, humidity, weather condition, wind speed, and timestamp.
- Added success/failure logging per city so a failed request wouldn't silently break the pipeline.

### 2. Transform
- Converted the list of extracted records into a Pandas DataFrame.
- Verified data types (temperature/wind speed as floats, humidity as integer, datetime as a true `datetime64` type — not just text).
- Renamed columns to be human-readable with units included (e.g. `Temperature (°C)`, `Wind Speed (m/s)`).

### 3. Load
- Saved the cleaned DataFrame to `data/weather_data.csv` for future analysis, with the row index excluded.

## Steps Taken

1. Created an OpenWeather account and generated a free API key.
2. Set up the project structure with a `.env` file for secure key storage.
3. Built and tested a single-city API call to inspect the raw JSON response.
4. Wrote an extraction function to flatten the nested JSON into a clean dictionary.
5. Looped the extraction across 3 cities into a list of records.
6. Converted the list into a structured, correctly typed, clearly labeled Pandas DataFrame.
7. Exported the DataFrame to CSV.
8. Ran comparative analysis (warmest/coolest city, most humid city, condition comparison).

## Key Findings

On 27 August 2026:
- **New York** was the warmest city at 22.3°C; **London** was the coolest at 19.16°C.
- **London** had the highest humidity (92%), well above Nairobi (56%) and New York (85%) — consistent with its overcast conditions.
- Weather conditions varied across all three cities: Nairobi (few clouds), London (overcast clouds), New York (scattered clouds).
- Temperature and humidity didn't move together — Nairobi wasn't the warmest city, but had by far the lowest humidity, reflecting its tropical highland climate.

## Project Structure
├── weather_etl.ipynb # Main ETL notebook
├── data/
│ └── weather_data.csv # Processed output dataset
├── .env # API key (excluded from repo)
├── .gitignore
└── README.md


## How to Run
1. Clone this repository.
2. Create a `.env` file in the project root with:

OPENWEATHER_API_KEY=your_api_key_here

3. Install dependencies:

pip install requests pandas python-dotenv

4. Run `weather_etl.ipynb` in Jupyter Notebook.

## Author

Tess Kamau
[LinkedIn](https://linkedin.com/in/tesskamau) | [GitHub](https://github.com/Tee-ai63)