<template>
  <main class="container text-white">
    <div class="pt-4 mb-8 relative">
      <input
        type="text"
        v-model="searchQuery"
        @input="getSearchResults"
        placeholder="Search for a city or state"
        class="py-2 px-1 w-full bg-transparent border-b focus:border-weather-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]"
      />
      <ul
        class="absolute bg-weather-secondary text-white w-full shadow-md py-2 px-1 top-[66px]"
        v-if="openWeatherSearchResults.length > 0 || searchError"
      >
        <p class="py-2" v-if="searchError">
          Sorry, something went wrong, please try again.
        </p>
        <p
          class="py-2"
          v-if="!searchError && openWeatherSearchResults.length === 0"
        >
          No results match your query, try a different term.
        </p>
        <template v-else>
          <li
            v-for="(searchResult, index) in openWeatherSearchResults"
            :key="index"
            class="py-2 cursor-pointer"
            @click="previewCity(searchResult)"
          >
            {{ searchResult.name }}, {{ searchResult.country }}
          </li>
        </template>
      </ul>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";
import { useRouter } from "vue-router";

const router = useRouter();
const searchQuery = ref(""); // Kullanıcıdan alınacak şehir adı
const queryTimeout = ref(null); 
const openWeatherSearchResults = ref([]); // Arama sonuçları
const searchError = ref(null); 


const openWeatherAPIKey = "9c1946f9c5ed61c27d9e64b636947851";

// Geocoding API'yi kullanarak şehir ismini alıp, enlem ve boylam bilgilerini alıyoruz
const getSearchResults = () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      try {
        const response = await axios.get(
          `http://api.openweathermap.org/geo/1.0/direct?q=${searchQuery.value}&limit=5&appid=${openWeatherAPIKey}`
        );
        openWeatherSearchResults.value = response.data;
        searchError.value = null;
      } catch (error) {
        searchError.value = true;
        openWeatherSearchResults.value = [];
      }
    } else {
      openWeatherSearchResults.value = [];
    }
  }, 300);
};

// Şehre tıklanınca detay sayfasına yönlendirme işlemi
const previewCity = (searchResult) => {
  const city = searchResult.name;
  const state = searchResult.state || "No State"; 

  // Yönlendirme
  router.push({
    name: "cityView",
    params: { city: city, state: state },
    query: {
      lat: searchResult.lat,
      lon: searchResult.lon,
      preview: true,
    },
  });
};
</script>
