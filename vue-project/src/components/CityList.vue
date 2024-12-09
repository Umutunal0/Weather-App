 <template>
        <div class="city-card" @click="$emit('click')">
          <h2>{{ city.name }}, {{ city.country }}</h2>
          <p>{{ Math.round(city.weather.main.temp) }}°C</p>
          <p>{{ city.weather.weather[0].description }}</p>
          <img
            :src="`http://openweathermap.org/img/wn/${city.weather.weather[0].icon}@2x.png`"
            alt="Weather icon"
          />
        </div>
    </template>
  
  <script setup>
  defineProps({
    city: Object,  // City bilgisini alıyoruz
  });
  </script>
  
  <style scoped>
  .city-card {
    cursor: pointer;
    border: 1px solid #ccc;
    padding: 16px;
    text-align: center;
    margin: 8px;
    background-color: #f9f9f9;
    border-radius: 8px;
  }
  
  .city-card img {
    width: 50px;
    height: 50px;
  }
  </style>
  