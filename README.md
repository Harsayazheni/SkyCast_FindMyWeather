# SkyCast - Find My Weather
## Date: 21-07-25
## Objective:
To build a responsive single-page application using React that allows users to enter a city name and retrieve real-time weather information using the OpenWeatherMap API. This project demonstrates the use of Axios for API calls, React Router for navigation, React Hooks for state management, controlled components with validation, and basic styling with CSS.
## Tasks:

#### 1. Project Setup
Initialize React app.

Install necessary dependencies: npm install axios react-router-dom

#### 2. Routing
Set up BrowserRouter in App.js.

Create two routes:

/ – Home page with input form.

/weather – Page to display weather results.

#### 3. Home Page (City Input)
Create a controlled input field for the city name.

Add validation to ensure the input is not empty.

On valid form submission, navigate to /weather and store the city name.

#### 4. Weather Page (API Integration)
Use Axios to fetch data from the OpenWeatherMap API using the city name.

Show temperature, humidity, wind speed, and weather condition.

Convert and display temperature in both Celsius and Fahrenheit using useMemo.

#### 5. React Hooks
Use useState for managing city, weather data, and loading state.

Use useEffect to trigger the Axios call on page load.

Use useCallback to optimize form submit handler.

Use useMemo for temperature conversion logic.

#### 6. UI Styling (CSS)
Create a responsive and clean layout using CSS.

Style form, buttons, weather display cards, and navigation links.

## Programs:
### App.jsx
```
import { Routes, Route } from 'react-router-dom'
import Home from './components/Home'
import Weather from './components/Weather'

export default function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/weather" element={<Weather />} />
    </Routes>
  )
}
```
### Main.jsx
```
import React from 'react'
import ReactDOM from 'react-dom/client'
import App from './App'
import { BrowserRouter } from 'react-router-dom'
import './index.css'

ReactDOM.createRoot(document.getElementById('root')).render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
)

```
### index.css
```
body {
  margin: 0;
  padding: 0;
  background: lightblue;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  text-align: center;
}

input {
  padding: 10px;
  margin-right: 5px;
}

button {
  background: darkblue;
  color: white;
  border: none;
}

.weather-card {
  padding: 20px;
  background: white;

  text-align: center;
}

```
### Home.jsx
```
import { useState, useCallback } from 'react'
import { useNavigate } from 'react-router-dom'

export default function Home() {
  const [city, setCity] = useState('')
  const navigate = useNavigate()

  const handleSubmit = useCallback((e) => {
    e.preventDefault()
    if (city.trim()) {
      navigate('/weather', { state: { city } })
    }
  }, [city])

  return (
    <div className="container">
      <h1>SkyCast</h1>
      <form onSubmit={handleSubmit}>
        <input value={city} onChange={(e) => setCity(e.target.value)} placeholder="Enter city" />
        <button type="submit">Get Weather</button>
      </form>
    </div>
  )
}

```
### Weather.jsx
```
import { useLocation } from 'react-router-dom'
import { useEffect, useState } from 'react'
import axios from 'axios'

export default function Weather() {
  const { state } = useLocation()
  const [data, setData] = useState(null)
  const [loading, setLoading] = useState(true)

  useEffect(() => {
    if (state?.city) {
      axios.get(`https://api.weatherapi.com/v1/current.json?key=5c90715be5954158a5295453251107&q=${state.city}`)
        .then(res => {
          setData(res.data)
          setLoading(false)
        })
    }
  }, [state?.city])

  if (loading) return <p>Loading...</p>

  return (
    <div className="weather-card">
      <h2>{data.location.name}, {data.location.country}</h2>
      <p>{data.current.condition.text}</p>
      <p>Temp: {data.current.temp_c}°C / {data.current.temp_f}°F</p>
      <p>Humidity: {data.current.humidity}%</p>
      <p>Wind: {data.current.wind_kph} km/h</p>
    </div>
  )
}

```
## Output:
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/73dbcd66-b76e-47a2-8370-74f928ce3133" />
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/b0694b72-8cce-4fd0-afbc-a008acbd7f02" />


## Result:
A responsive single-page application using React that allows users to enter a city name and retrieve real-time weather information using the OpenWeatherMap API has been built successfully. 
