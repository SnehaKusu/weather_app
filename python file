from flask import Flask, render_template, request
import requests

app = Flask(__name__)

# Replace 'your_api_key' with your actual OpenWeatherMap API key
API_KEY = '644fd592fe1c122fa91b2b12b0327be7'

# Route for the homepage
@app.route('/')
def index():
    return render_template('index.html')

# Route to handle the form submission and get the weather
@app.route('/weather', methods=['POST'])
def get_weather():
    city = request.form['city']  # Get the city from the form input
    weather = fetch_weather_data(city)
    
    if weather:
        return render_template('result.html', weather=weather)
    else:
        return render_template('index.html', error="City not found!")

def fetch_weather_data(city):
    # OpenWeatherMap API URL
    url = f"http://api.openweathermap.org/data/2.5/weather?q={city}&appid={API_KEY}&units=metric"
    response = requests.get(url)
    
    if response.status_code == 200:
        data = response.json()
        return {
            'city': data['name'],
            'temperature': data['main']['temp'],
            'description': data['weather'][0]['description'],
            'humidity': data['main']['humidity'],
            'wind_speed': data['wind']['speed']
        }
    else:
        return None

if __name__ == '__main__':
    app.run(debug=True)
