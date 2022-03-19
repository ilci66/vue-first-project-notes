<template>
  <div class="card">
    <h3 v-if="digimon">{{digimon.name}}</h3>
    <img class="card-image" src="https://digimon.shadowsmith.com/img/otamamon.jpg" alt="cool digimon" srcset="">
    <h3 class="digimon-name">some digimon</h3>
    <p class="digimon-level">digimon level</p>
    
  </div>
</template>

<script>
  export default {
    props:["digimon"]
  }
</script>

<style scoped>
  .card{
    margin: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    background: rgba(0,0,0,0.25);
    padding: 15px;
    border-radius: 5px;
    transition: 0.4s;
  }
  .card:hover{
    box-shadow:0 0 16px rgba(255,255,255,1);
    cursor: pointer;
  }
  .card-image{
    width: 80%;
  }
</style>