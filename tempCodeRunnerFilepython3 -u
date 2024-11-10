from flask import Flask, render_template, request
import requests
from dotenv import load_dotenv
import os

# Load environment variables from .env file
load_dotenv()

app = Flask(__name__)

API_KEY = os.getenv('API_KEY')  # Fetch the API key from the environment

@app.route('/', methods=['GET', 'POST'])
def home():
    weather = ""
    temp = ""
    country = ""
    if request.method == 'POST':
        user_input = request.form['city']
        weather_data = requests.get(
            f"https://api.openweathermap.org/data/2.5/weather?q={user_input}&units=metric&APPID={API_KEY}"
        )
        if weather_data.status_code == 200:
            data = weather_data.json()
            weather = data['weather'][0]['main']
            temp = data["main"]['temp']
            country = data['sys']["country"]
        else:
            weather = "City not found!"
    
    return render_template('index.html', weather=weather, temp=temp, country=country)

if __name__ == '__main__':
    app.run(debug=True)
