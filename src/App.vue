<template>
  <div class ="weather-app">
    <SearchBar @search="handleSearch" />

    <div v-if="hasError" class="weather-app__error-message">
      <p>Data not found. Please enter a valid city name.</p>
    </div>

    <div v-else>
      <h2 class="weather-app__city">{{ city }}</h2>
      <div class="weather-app__cards">
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
.weather-app{
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 80px;

&__cards {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  justify-content: center;
  margin-top: 1rem;
}
&__city {
  margin-top: 10px;
  margin-bottom: 10px;
  font-size: 1.9rem;
  font-weight: 600;
  color: rgb(4, 32, 67);
  text-align: center;
}
}
</style>
