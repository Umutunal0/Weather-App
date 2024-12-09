<template>
  <div class="container text-white">
    <h1 class="text-4xl mb-4">{{ city }} Weather</h1>

    <div v-if="weatherData">
      <p class="text-2xl">Current Temperature: {{ Math.round(weatherData.current.temp) }}°C</p>
      <p>{{ weatherData.current.weather[0].description }}</p>
      <img
        :src="`http://openweathermap.org/img/wn/${weatherData.current.weather[0].icon}@2x.png`"
        alt="Weather Icon"
        class="w-[100px] h-[100px]"
      />
    </div>

    <div v-if="hourlyWeatherData">
      <h2 class="text-xl">Hourly Forecast</h2>
      <ul>
        <li v-for="(hour, index) in hourlyWeatherData" :key="index">
          {{ new Date(hour.dt * 1000).toLocaleTimeString() }} - {{ Math.round(hour.temp) }}°C
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import { useRoute } from "vue-router";

const route = useRoute();
const city = route.params.city; // Şehir adı
const state = route.params.state || "Unknown"; 

const lat = route.query.lat;


const weatherData = ref(null); // Güncel hava durumu için
const hourlyWeatherData = ref([]); // Saatlik hava durumu için

// One Call API 3.0'ı kullanarak hava durumu verisini alındı
const fetchWeatherData = async () => {
  try {
    const response = await axios.get(
      `https://api.openweathermap.org/data/3.0/onecall?lat=${lat}&lon=
      ${lon}&exclude=minutely&appid=9c1946f9c5ed61c27d9e64b636947851&units=metric`
    );
    weatherData.value = response.data;
    hourlyWeatherData.value = response.data.hourly;
  } catch (error) {
    console.error("Error fetching weather data:", error);
  }
};

// Sayfa yüklendiğinde hava durumu verilerini al
onMounted(fetchWeatherData);
</script>
