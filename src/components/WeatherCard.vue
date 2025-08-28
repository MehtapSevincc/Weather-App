<template>
    <div class="weather-card">
        <h3>{{ formattedDate }}</h3>
        <p>{{ conditionText }}</p>
        <p>{{ temp }} °C</p>
    </div>
</template>
<script>
export default {
    name: 'WeatherCard',
    props: {
        date: {
            type: String,
            required: true,
        },
        conditionText:{
            type: String,
            required: true,
        },
        temp :{
            type: Number,
            required: true,
        },
    },
    computed:{
        formattedDate(){
            return this.date;
        },
    },
};
</script>