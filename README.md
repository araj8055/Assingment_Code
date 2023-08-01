# Assingment_Code
import requests
API_KEY =  '76b823308dcac64c1499b1827abf66d4' #API_KEY Value
BASE_URL = 'https://api.openweathermap.org/data/2.5/forecast'

def get_weather(location, date):
    url = f'{BASE_URL}?q={location}&appid={API_KEY}'
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        for item in data['list']:
            if item['dt_txt'].startswith(date):
                return item['main']['temp']
    else:
        print(f"Error fetching weather data. Status code: {response.status_code}")
    return None

def get_wind_speed(location, date):
    url = f'{BASE_URL}?q={location}&appid={API_KEY}'
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        for item in data['list']:
            if item['dt_txt'].startswith(date):
                return item['wind']['speed']
    else:
        print(f"Error fetching weather data. Status code: {response.status_code}")
    return None

def get_pressure(location, date):
    url = f'{BASE_URL}?q={location}&appid={API_KEY}'
    response = requests.get(url)
    if response.status_code == 200:
        data = response.json()
        for item in data['list']:
            if item['dt_txt'].startswith(date):
                return item['main']['pressure']
    else:
        print(f"Error fetching weather data. Status code: {response.status_code}")
    return None

def main():
    print("Welcome to Weather Forecast!")
    while True:
        print("\nOptions:")
        print("1. Get weather")
        print("2. Get Wind Speed")
        print("3. Get Pressure")
        print("0. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            location = input("Enter the location (e.g., London,us): ")
            date = input("Enter the date (YYYY-MM-DD): ")
            temperature = get_weather(location, date)
            if temperature is not None:
                print(f"Temperature on {date}: {temperature} Kelvin")
            else:
                print("Data not available for the input date.")
        elif choice == '2':
            location = input("Enter the location (e.g., London,us): ")
            date = input("Enter the date (YYYY-MM-DD): ")
            wind_speed = get_wind_speed(location, date)
            if wind_speed is not None:
                print(f"Wind Speed on {date}: {wind_speed} m/s")
            else:
                print("Data not available for the input date.")
        elif choice == '3':
            location = input("Enter the location (e.g., London,us): ")
            date = input("Enter the date (YYYY-MM-DD): ")
            pressure = get_pressure(location, date)
            if pressure is not None:
                print(f"Pressure on {date}: {pressure} hPa")
            else:
                print("Data not available for the input date.")
        elif choice == '0':
            print("Exiting the program.")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
