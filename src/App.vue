<template>
    <div id="app">
        <SearchBar @search ="handleSearch"/>
        <div class="weather-cards">
            <WeatherCard
            v-for="day in forecast"
            :key ="day.date"
            :date="day.date"
            :conditionText="day.condition.text"
            :temp="day.temp_c"
            />
        </div>
    </div>
</template>

<script>
import axios from 'axios';
import SearchBar from './components/SearchBar.vue';
import WeatherCard from './components/WeatherCard.vue';

export default {
    components: {SearchBar,WeatherCard},
    data(){
        return {
            city:'Istanbul',
            forecast:[],
            apiKey:'350e231fb54d4a74ac1172741252708'
        };
    },
    methods:{
        async fetchWeather(city){
            try{
                const response = await axios.get('https://api.weatherapi.com/v1/forecast.json',{
                    params: {
                        key:this.apiKey,
                        q: city,
                        days:4,
                        aqi:'no',
                        alerts:'no'


                    }

                });
            
                this.forecast = response.data.forecast.forecastday;

            }
            catch (error){
                console.error('Hava durumu verisi alınamadı:',error);
                this.forecast =[];
            }
        },
        handleSearch(newCity) {
            this.city =newCity;
            this.fetchWeather(this.city);
        }
    },
    mounted(){
        this.fetchWeather(this.city);
    }
};
</script>  
<style scoped>
.weather-cards{
    display: flex;
    flex-wrap:wrap;
    gap: 1rem;
    justify-content: center;
    margin-top: 1rem;
}
</style>