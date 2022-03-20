<template>
  <div class="current-digimon-container" >
    <img lazy class="selected-digimon-img" v-if="selected" :src="selected['0'].img" alt="some digimon">
    <p v-if="selected">{{selected["0"].name}}</p>
    <p v-if="!selected">Digimon will appear here with the image</p>
    <p v-if="selected">{{selected["0"].level}}</p>
    <button @click="$emit('add', selected['0'])" class="pokemon-add-button" v-if="selected">Add</button>
  </div>
</template>

<script>
  export default {
    methods: {
    },
    props: ["selected", "toAdd"]
  }
</script>

<style scoped>
.current-digimon-container {
  height: 300px;
  min-width: 240px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
@media (max-width: 600px) {
  .current-digimon-container {
      grid-column: 1/ -1;
      margin-top: 10px;
  }
}
.selected-digimon-img{
  height: 200px;
  object-fit: cover;
  max-width: 300px;
  border-radius: 15px;
}
.pokemon-add-button{
  padding: 10px 5px;
  border-radius: 5px;
  border:none;
  color: rgb(31, 143, 31);
  background: white;
  font-weight: bold;
  font-size: 20px;
  transition: 0.4s;
}
.pokemon-add-button:hover{
  box-shadow: 0 0 16px white;
  cursor: pointer
}
</style>