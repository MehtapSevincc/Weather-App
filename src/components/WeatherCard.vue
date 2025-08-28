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

<style scoped lang="scss">
.weather-card {
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  padding: 1rem;
  width: 160px;
  text-align: center;
  transition: transform 0.2s ease;
 

  &:hover {
    transform: scale(1.03);
    background-color: rgb(237, 233, 233);
  }

  h3 {
    margin-bottom: 0.5rem;
    font-size: 1rem;
  }

  p {
    margin: 0.3rem 0;
    font-size: 0.95rem;
  }
}
</style>

