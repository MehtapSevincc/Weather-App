<template>
  <div class="search-bar">
    <input
    class="search-bar__input"
      v-model="cityInput"
      @keyup.enter="emitSearch"
      type="text"
      placeholder="Enter a city (e.g. Ankara)"
    />
    <button class ="search-bar__button" @click="emitSearch">
      <i class=" search-bar__icon fa-solid fa-magnifying-glass"></i>
    </button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      cityInput: "",
    };
  },
  methods: {
    emitSearch() {
      if (this.cityInput.trim()) {
        this.$emit("search", this.cityInput.trim());
        this.cityInput = "";
      }
    },
  },
};
</script>

<style scoped lang="scss">
.search-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
  gap: 8px;

  &__input {
    padding: 0.6rem 1rem;
    font-size: 1.1rem;
    border: 1px solid #ccc;
    border-radius: 8px;
    width: 260px;
    outline: none;
    transition: box-shadow 0.2s ease;

    &:focus {
      box-shadow: 0 0 0 2px #0077ff33;
    }
  }

  &__button {
    padding: 0.6rem 1rem;
    font-size: 1.1rem;
    border: none;
    background-color: #2874ca;
    color: white;
    border-radius: 8px;
    cursor: pointer;
    transition: background-color 0.2s ease;

    &:hover {
      background-color: #005fcc;
    }
 }
    &__icon {
      pointer-events: none;
    }
 
}
</style>
