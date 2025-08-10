# Task1
Api integration 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Weather App</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(135deg, #00c6ff, #0072ff);
            color: white;
            text-align: center;
        }
        header {
            padding: 1rem;
            background: rgba(0, 0, 0, 0.3);
        }
        .container {
            max-width: 500px;
            margin: auto;
            padding: 1rem;
        }
        input {
            padding: 10px;
            width: 70%;
            border: none;
            border-radius: 5px;
            margin-bottom: 1rem;
        }
        button {
            padding: 10px 15px;
            border: none;
            border-radius: 5px;
            background: #ff9800;
            color: white;
            cursor: pointer;
        }
        .weather-card {
            margin-top: 1rem;
            padding: 20px;
            border-radius: 10px;
            background: rgba(0, 0, 0, 0.4);
        }
        @media (max-width: 600px) {
            input {
                width: 60%;
            }
        }
    </style>
</head>
<body>
    <header>
        <h1>Weather App</h1>
    </header>

    <div class="container">
        <input type="text" id="city" placeholder="Enter city name">
        <button onclick="getWeather()">Get Weather</button>

        <div id="weatherResult" class="weather-card" style="display: none;"></div>
    </div>

    <script>
        const API_KEY = "YOUR_API_KEY"; // Get from https://openweathermap.org/api

        async function getWeather() {
            const city = document.getElementById("city").value;
            if (!city) {
                alert("Please enter a city name.");
                return;
            }

            const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${API_KEY}&units=metric`;

            try {
                const response = await fetch(url);
                if (!response.ok) throw new Error("City not found");
                const data = await response.json();

                document.getElementById("weatherResult").style.display = "block";
                document.getElementById("weatherResult").innerHTML = `
                    <h2>${data.name}, ${data.sys.country}</h2>
                    <p>🌡 Temperature: ${data.main.temp}°C</p>
                    <p>🌤 Weather: ${data.weather[0].description}</p>
                    <p>💨 Wind Speed: ${data.wind.speed} m/s</p>
                `;
            } catch (error) {
                alert(error.message);
            }
        }
    </script>
</body>
</html>
