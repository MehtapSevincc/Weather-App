<template>
    <div class="search-bar">
        <input 
        v-model="cityInput"
        @keyup.enter="emitSearch"
        type="text"
        placeholder="Enter a city (e.g. Ankara)"/>
        <button @click="emitSearch"><i class="fa-solid fa-magnifying-glass"></i></button>
    </div>
</template>
<script>
export default {
    data() {
        return {
            cityInput:''
        };
    },
    methods :{
        emitSearch(){
            if (this.cityInput.trim()){
                this.$emit('search',this.cityInput.trim());
                this.cityInput = '';

            }
        }
    }
};
</script>


