# fatoshhh

<!DOCTYPE html>
<html lang="kk">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>FATOSHH | Weather</title>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'Inter', sans-serif;
  min-height: 100vh;
  color: white;
  background:
    radial-gradient(circle at 10% 10%, #254c82 0%, transparent 35%),
    radial-gradient(circle at 90% 80%, #482a78 0%, transparent 35%),
    #080e1e;
  padding: 30px 7%;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 55px;
}

.logo {
  font-size: 29px;
  font-weight: 800;
  letter-spacing: 3px;
}

.logo span {
  color: #6ab8ff;
}

.tag {
  color: #a9bad3;
  font-size: 13px;
}

.container {
  max-width: 1000px;
  margin: auto;
}

.search {
  display: flex;
  gap: 12px;
  margin-bottom: 35px;
}

.search input {
  flex: 1;
  padding: 17px 20px;
  border-radius: 15px;
  border: 1px solid #34435d;
  background: #18243a;
  color: white;
  outline: none;
  font-size: 15px;
}

.search button {
  padding: 0 25px;
  border: none;
  border-radius: 15px;
  background: #419bff;
  color: white;
  font-weight: 700;
  cursor: pointer;
}

.search button:hover {
  background: #1978e5;
}

.main-card {
  padding: 40px;
  border-radius: 28px;
  background: linear-gradient(135deg,
    rgba(54, 115, 190, .35),
    rgba(43, 37, 83, .55));
  border: 1px solid rgba(255,255,255,.12);
  box-shadow: 0 20px 60px #0005;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 20px;
}

.city {
  font-size: 27px;
  font-weight: 700;
}

.date {
  color: #bdcce0;
  margin-top: 12px;
  font-size: 14px;
}

.temp {
  font-size: 85px;
  font-weight: 800;
  letter-spacing: -5px;
}

.weather-icon {
  font-size: 75px;
}

.description {
  color: #d3e4fa;
  font-size: 16px;
  margin-top: 5px;
}

.section-title {
  margin: 38px 0 20px;
  font-size: 20px;
}

.stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}

.stat {
  background: rgba(255,255,255,.07);
  padding: 23px;
  border: 1px solid #ffffff15;
  border-radius: 20px;
}

.stat-icon {
  font-size: 25px;
}

.stat h3 {
  color: #aabbd2;
  font-size: 13px;
  margin: 15px 0 8px;
}

.stat p {
  font-size: 23px;
  font-weight: 700;
}

.forecast {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 13px;
}

.day {
  text-align: center;
  padding: 20px 8px;
  border-radius: 18px;
  background: rgba(255,255,255,.07);
  border: 1px solid #ffffff12;
}

.day p {
  color: #bdcce0;
  font-size: 13px;
}

.day .icon {
  font-size: 32px;
  margin: 16px 0;
}

.day strong {
  font-size: 16px;
}

footer {
  text-align: center;
  margin-top: 55px;
  color: #7185a3;
  font-size: 12px;
  letter-spacing: 2px;
}

#message {
  color: #ffb5b5;
  margin: 12px 5px;
}

@media(max-width:600px) {
  body { padding: 22px 5%; }
  header { margin-bottom: 35px; }
  .tag { display: none; }
  .main-card { padding: 25px; }
  .temp { font-size: 65px; }
  .stats { grid-template-columns: 1fr 1fr; }
  .forecast { grid-template-columns: repeat(2, 1fr); }
  .search button { padding: 0 15px; }
}
</style>
</head>

<body>

<header>
  <div class="logo">FATO<span>SHH</span></div>
  <div class="tag">WEATHER EXPERIENCE ✦</div>
</header>

<div class="container">

  <div class="search">
    <input id="cityInput" placeholder="Қаланы енгізіңіз..." value="Almaty">
    <button onclick="searchWeather()">Іздеу</button>
  </div>

  <div id="message"></div>

  <div class="main-card">
    <div>
      <div class="city" id="city">Almaty, Kazakhstan</div>
      <div class="date" id="date"></div>
      <div class="temp" id="temp">--°</div>
      <div class="description" id="description">Жүктелуде...</div>
    </div>
    <div class="weather-icon" id="weatherIcon">🌤️</div>
  </div>

  <h2 class="section-title">Бүгінгі көрсеткіштер</h2>

  <div class="stats">
    <div class="stat">
      <div class="stat-icon">🌡️</div>
      <h3>Сезілетін температура</h3>
      <p id="feels">--°C</p>
    </div>

    <div class="stat">
      <div class="stat-icon">💧</div>
      <h3>Ылғалдылық</h3>
      <p id="humidity">--%</p>
    </div>

    <div class="stat">
      <div class="stat-icon">💨</div>
      <h3>Жел жылдамдығы</h3>
      <p id="wind">-- km/h</p>
    </div>
  </div>

  <h2 class="section-title">📅 5 күндік болжам</h2>

  <div class="forecast" id="forecast"></div>

</div>

<footer>
  © 2026 FATOSHH WEATHER · MADE WITH ❤️
</footer>

<script>
const weatherTypes = {
  0: ["Ашық аспан", "☀️"],
  1: ["Көбіне ашық", "🌤️"],
  2: ["Ала бұлтты", "⛅"],
  3: ["Бұлтты", "☁️"],
  45: ["Тұман", "🌫️"],
  48: ["Қыраулы тұман", "🌫️"],
  51: ["Сіркіреме жаңбыр", "🌦️"],
  53: ["Жаңбыр", "🌧️"],
  55: ["Қатты сіркіреме", "🌧️"],
  61: ["Аздаған жаңбыр", "🌦️"],
  63: ["Жаңбыр", "🌧️"],
  65: ["Қатты жаңбыр", "🌧️"],
  71: ["Қар", "🌨️"],
  73: ["Қар жауып тұр", "❄️"],
  75: ["Қатты қар", "❄️"],
  80: ["Нөсер", "🌧️"],
  81: ["Қатты нөсер", "🌧️"],
  82: ["Өте қатты нөсер", "⛈️"],
  95: ["Найзағай", "⛈️"],
  96: ["Бұршақ", "⛈️"],
  99: ["Қатты найзағай", "⛈️"]
};

function getWeather(code) {
  return weatherTypes[code] || ["Ауа райы", "🌤️"];
}

const days = [
  "Жексенбі", "Дүйсенбі", "Сейсенбі",
  "Сәрсенбі", "Бейсенбі", "Жұма", "Сенбі"
];

async function searchWeather() {
  const cityName = document.getElementById("cityInput").value.trim();
  const message = document.getElementById("message");

  if (!cityName) {
    message.textContent = "Қала атауын енгізіңіз!";
    return;
  }

  message.textContent = "Ауа райы жүктелуде...";

  try {
    const geoUrl =
      `https://geocoding-api.open-meteo.com/v1/search?name=${encodeURIComponent(cityName)}&count=1&language=kk&format=json`;

    const geoResponse = await fetch(geoUrl);
    const geoData = await geoResponse.json();

    if (!geoData.results || !geoData.results.length) {
      throw new Error("Қала табылмады!");
    }

    const place = geoData.results[0];

    const url =
      `https://api.open-meteo.com/v1/forecast?latitude=${place.latitude}&longitude=${place.longitude}&current=temperature_2m,relative_humidity_2m,apparent_temperature,is_day,precipitation,weather_code,wind_speed_10m&daily=weather_code,temperature_2m_max,temperature_2m_min&timezone=auto&forecast_days=5`;

    const response = await fetch(url);
    const data = await response.json();

    const current = data.current;
    const daily = data.daily;

    document.getElementById("city").textContent =
      `${place.name}, ${place.country}`;

    document.getElementById("date").textContent =
      new Date().toLocaleDateString("kk-KZ", {
        weekday: "long",
        day: "numeric",
        month: "long"
      });

    document.getElementById("temp").textContent =
      Math.round(current.temperature_2m) + "°";

    const weather = getWeather(current.weather_code);

    document.getElementById("description").textContent =
      weather[0];

    document.getElementById("weatherIcon").textContent =
      current.is_day ? weather[1] :
      (current.weather_code === 0 ? "🌙" : weather[1]);

    document.getElementById("feels").textContent =
      Math.round(current.apparent_temperature) + "°C";

    document.getElementById("humidity").textContent =
      current.relative_humidity_2m + "%";

    document.getElementById("wind").textContent =
      current.wind_speed_10m + " km/h";

    let html = "";

    daily.time.forEach((date, i) => {
      const d = new Date(date + "T12:00:00");
      const w = getWeather(daily.weather_code[i]);

      html += `
        <div class="day">
          <p>${i === 0 ? "Бүгін" : days[d.getDay()]}</p>
          <div class="icon">${w[1]}</div>
          <strong>
            ${Math.round(daily.temperature_2m_max[i])}°
            /
            ${Math.round(daily.temperature_2m_min[i])}°
          </strong>
        </div>
      `;
    });

    document.getElementById("forecast").innerHTML = html;
    message.textContent = "";

  } catch (error) {
    message.textContent = error.message ||
      "Қате орын алды. Интернетті тексеріңіз.";
  }
}

document.getElementById("cityInput")
  .addEventListener("keydown", e => {
    if (e.key === "Enter") searchWeather();
  });

searchWeather();
</script>

</body>
</html>
