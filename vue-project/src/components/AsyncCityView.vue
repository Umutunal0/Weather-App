<template>
    <div class="flex flex-col items-center">
      <!-- Loading Skeleton (Veri Gelene Kadar Gösterilecek) -->
      <div v-if="!weatherData" class="animate-pulse">
        <div class="w-32 h-32 bg-gray-300 rounded-full"></div>
        <div class="w-48 h-4 bg-gray-300 mt-4 rounded"></div>
        <div class="w-32 h-4 bg-gray-300 mt-2 rounded"></div>
      </div>
  
      <!-- Weather Data -->
      <div v-else>
        <h1 class="text-4xl mb-2">{{ route.params.city }}</h1>
        <p class="text-sm mb-12">
          {{
            new Date(weatherData.currentTime).toLocaleDateString("en-us", {
              weekday: "short",
              day: "2-digit",
              month: "long",
            })
          }}
          {{
            new Date(weatherData.currentTime).toLocaleTimeString("en-us", {
              timeStyle: "short",
            })
          }}
        </p>
        <p class="text-8xl mb-8">
          {{ Math.round(weatherData.current.temp) }}&deg;
        </p>
        <p>Feels like {{ Math.round(weatherData.current.feels_like) }} &deg;</p>
        <p class="capitalize">{{ weatherData.current.weather[0].description }}</p>
        <img
          class="w-[150px] h-auto"
          :src="`http://openweathermap.org/img/wn/${weatherData.current.weather[0].icon}@2x.png`"
          alt="Weather Icon"
        />
  
        <!-- Hourly Weather -->
        <div class="max-w-screen-md w-full py-12">
          <h2 class="mb-4 text-white">Hourly Weather</h2>
          <div class="flex gap-10 overflow-x-scroll">
            <div
              v-for="hourData in weatherData.hourly"
              :key="hourData.dt"
              class="flex flex-col gap-4 items-center"
            >
              <p class="whitespace-nowrap text-md">
                {{
                  new Date(hourData.currentTime).toLocaleTimeString("en-us", {
                    hour: "numeric",
                  })
                }}
              </p>
              <img
                class="w-auto h-[50px] object-cover"
                :src="`http://openweathermap.org/img/wn/${hourData.weather[0].icon}@2x.png`"
                alt="Hour Weather Icon"
              />
              <p class="text-xl">{{ Math.round(hourData.temp) }}&deg;</p>
            </div>
          </div>
        </div>
  
        <!-- Weekly Weather -->
        <div class="max-w-screen-md w-full py-12">
          <h2 class="mb-4 text-white">7 Day Forecast</h2>
          <div v-for="day in weatherData.daily" :key="day.dt" class="flex items-center">
            <p class="flex-1">
              {{
                new Date(day.dt * 1000).toLocaleDateString("en-us", {
                  weekday: "long",
                })
              }}
            </p>
            <img
              class="w-[50px] h-[50px] object-cover"
              :src="`http://openweathermap.org/img/wn/${day.weather[0].icon}@2x.png`"
              alt="Day Weather Icon"
            />
            <div class="flex gap-2 flex-1 justify-end">
              <p>H: {{ Math.round(day.temp.max) }}</p>
              <p>L: {{ Math.round(day.temp.min) }}</p>
            </div>
          </div>
        </div>
  
        <!-- Remove City Button -->
        <div class="flex items-center gap-2 py-12 text-white cursor-pointer duration-150 hover:text-red-500" @click="removeCity">
          <i class="fa-solid fa-trash"></i>
          <p>Remove City</p>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from "vue";
  import { useRoute, useRouter } from "vue-router";
  import axios from "axios";
  
  const route = useRoute();
  const router = useRouter();
  
  
  const openWeatherAPIKey = "9c1946f9c5ed61c27d9e64b636947851";// OpenWeather API anahtarı
  const weatherData = ref(null);
  
  // Şehir için hava durumu verilerini çekme fonksiyonu
  const fetchWeatherData = async () => {
    try {
      const { data } = await axios.get(
        `https://api.openweathermap.org/data/2.5/onecall?lat=${route.query.lat}&lon=
        ${route.query.lng}&exclude=minutely,hourly&appid=${openWeatherAPIKey}&units=metric`
      );
      weatherData.value = data;
    } catch (error) {
      console.error("Error fetching weather data:", error);
    }
  };
  onMounted(fetchWeatherData);
  
  // Şehri kaldırma işlemi
  const removeCity = () => {
    const cities = JSON.parse(localStorage.getItem("savedCities"));
    const updatedCities = cities.filter((city) => city.id !== route.query.id);
    localStorage.setItem("savedCities", JSON.stringify(updatedCities));
    router.push({
      name: "home",
    });
  };
  </script>
  