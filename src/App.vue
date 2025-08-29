<template>
  <div id="app">
    <SearchBar @search="handleSearch" />

    <div v-if="hasError" class="error-message">
      <p>Data not found. Please enter a valid city name.</p>
    </div>

    <div v-else>
      <h2>{{ city }}</h2>
      <div class="weather-cards">
        <WeatherCard
          v-for="day in forecast"
          :key="day.date"
          :date="day.date"
          :conditionText="day.day ? day.day.condition.text : ''"
          :temp="day.day ? day.day.avgtemp_c : ''"
          :conditionIcon="day.day ? day.day.condition.icon : ''"
        />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import SearchBar from "./components/SearchBar.vue";
import WeatherCard from "./components/WeatherCard.vue";

export default {
  components: { SearchBar, WeatherCard },
  data() {
    return {
      city: "Istanbul",
      forecast: [],
      apiKey: import.meta.env.VITE_API_KEY,
      hasError: false,
    };
  },
  methods: {
    async fetchWeather(city) {
      try {
        const response = await axios.get(
          "https://api.weatherapi.com/v1/forecast.json",
          {
            params: {
              key: this.apiKey,
              q: city,
              days: 4,
              aqi: "no",
              alerts: "no",
            },
          }
        );

        this.forecast = response.data.forecast.forecastday;
        this.city = response.data.location.name;
        this.hasError = false;
      } catch (error) {
        console.error("Hava durumu verisi alınamadı:", error);
        this.forecast = [];
        this.city = "";
        this.hasError = true;
      }
    },
    handleSearch(newCity) {
      this.fetchWeather(newCity);
    },
  },
  mounted() {
    this.fetchWeather(this.city);
  },
};
</script>
<style scoped lang="scss">
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 80px;
}
.weather-cards {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
  margin-top: 1rem;
}
h2 {
  margin-top: 10px;
  margin-bottom: 10px;
  font-size: 1.9rem;
  font-weight: 600;
  color: rgb(4, 32, 67);
  text-align: center;
}
</style>
