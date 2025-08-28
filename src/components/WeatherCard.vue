<template>
  <div style="border: 1px solid black; padding: 1rem;">
    <p>{{ date }}</p>
    <p>{{ conditionText }}</p>
    <p>{{ temp }}°C</p>
  </div>
</template>

<script>
export default {
  props: ['date', 'conditionText', 'temp']
}
</script>
