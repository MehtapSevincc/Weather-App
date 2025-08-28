<template>
    <div class="weather-card">
        <h3>{{ formattedDate }}</h3>
       <img :src="iconUrl" alt="weather icon" />
        <p>{{ conditionText }}</p>
        <p>{{ temp }} °C</p>
    </div>
</template>
<script>
export default {
    name: 'WeatherCard',
    props: {
        date: String,
         conditionText: String,  
         temp :  Number,
        conditionIcon: String
    },
    computed:{
        formattedDate(){
            return this.date;
        },
        iconUrl(){
            if(!this.conditionIcon) return '';
            return this.conditionIcon.startsWith('http') ? this.conditionIcon :`https:${this.conditionIcon}`;
        }
    }
};
</script>