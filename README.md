# Weather-Application-in-Python-that-connects-to-a-Public-Weather-API
 App allows users to input a location (city or coordinates) and fetch real-time weather data, including temperature, humidity, and wind speed. The app will display the weather information in a user-friendly format.

#Fetching Weather Data
import requests

def get_weather(city_name, api_key):
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city_name}&appid={api_key}&units=metric"
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        return {
            "temperature": data["main"]["temp"],
            "humidity": data["main"]["humidity"],
            "wind_speed": data["wind"]["speed"]
        }
    else:
        return {"error": response.json().get("message", "Unable to fetch weather data")}



#Console UI
def main():
    api_key = "your_api_key_here"
    print("Welcome to the Weather App!")
    while True:
        city = input("Enter a city name (or type 'exit' to quit): ")
        if city.lower() == "exit":
            print("Goodbye!")
            break
        weather = get_weather(city, api_key)
        if "error" in weather
            print(f"Error: {weather['error']}")
        else:
            print(f"Temperature: {weather['temperature']}°C")
            print(f"Humidity: {weather['humidity']}%")
            print(f"Wind Speed: {weather['wind_speed']} m/s")



#Logging
import logging

logging.basicConfig(filename='weather_app.log', level=logging.INFO)

def log_message(message):
    logging.info(message)



#SQ Lite Integration
import sqlite3

def init_db():
    conn = sqlite3.connect("weather_history.db")
    cursor = conn.cursor()
    cursor.execute("""
        CREATE TABLE IF NOT EXISTS history (
            id INTEGER PRIMARY KEY,
            city TEXT,
            temperature REAL,
            humidity REAL,
            wind_speed REAL,
            timestamp DATETIME DEFAULT CURRENT_TIMESTAMP
        )
    """)
    conn.commit()
    conn.close()

def save_to_db(city, temperature, humidity, wind_speed):
    conn = sqlite3.connect("weather_history.db")
    cursor = conn.cursor()
    cursor.execute("""
        INSERT INTO history (city, temperature, humidity, wind_speed)
        VALUES (?, ?, ?, ?)
    """, (city, temperature, humidity, wind_speed))
    conn.commit()
    conn.close()






 #
