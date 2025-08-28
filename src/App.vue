<template>
    <div id="app">
        <SearchBar @search ="handleSearch"/>
        <h2> {{ city }}</h2>
        <div class="weather-cards">
            <WeatherCard
            v-for="day in forecast"
            :key ="day.date"
            :date="day.date"
            :conditionText=" day.day ? day.day.condition.text : ''"
            :temp="day.day ? day.day.avgtemp_c :''"
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
                const response = await axios.get('http://api.weatherapi.com/v1/forecast.json',{
                    params: {
                        key:this.apiKey,
                        q: city,
                        days:4,
                        aqi:'no',
                        alerts:'no'


                    }

                });
            
                this.forecast = response.data.forecast.forecastday;
                this.city = response.data.location.name;
            }
            catch (error){
                console.error('Hava durumu verisi alınamadı:',error);
                this.forecast =[];
            }
        },
        handleSearch(newCity) {
           
            this.fetchWeather(newCity);
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