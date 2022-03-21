<template>
  <div class="card">
    <img class="card-image" :src="digimon.img" alt="cool digimon">
    <h3 class="digimon-name">{{digimon.name}}</h3>
    <p class="digimon-level">{{digimon.level}}</p>
    <button @click="$emit('remove', digimon.name)" class="remove-button">Remove</button>
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
  .remove-button{
    border: none;
    padding: 5px;
    width: 100%;
    background: rgb(173, 8, 8);
    border-radius: 5px;
    color: whitesmoke;
    font-size: 1.2rem;
    margin-top: 10px;
    transition: 0.4s;
  }
  .remove-button:hover{
    box-shadow: 0 0 16px rgb(250, 25, 25);
    cursor: pointer;
  }
</style>