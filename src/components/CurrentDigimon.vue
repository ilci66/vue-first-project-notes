<template>
  <div class="current-digimon-container">
    the current pokemon
  </div>
</template>

<script>
  export default {
      
  }
</script>

<style scoped>
.current-digimon-container {
  height: 300px;
  width: 30%;
  background: rgba(0,0,0,0.25);
  margin: 0 auto;
}
@media (max-width: 600px) {
  .current-digimon-container {
    width: 100%;
  }
}
</style>