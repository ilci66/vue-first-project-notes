<template>
  <div class="collection-container">
    <DigimonCardVue v-for="digimon in digimons" :key="digimon.name"/>
  </div>

</template>

<script>
  import DigimonCardVue from "./DigimonCard.vue"

  export default {
    components:{
      DigimonCardVue
    },
    data() {
      return {
        digimons: [
          {"name": "digi1", "level": "awesome"},
          {"name": "digi2", "level": "cool"},
          {"name": "digi3", "level": "superb"},
          {"name": "digi4", "level": "awesome"},
          {"name": "digi5", "level": "cool"},
        ]
      }
    }
  }
</script>

<style scoped>
  .collection-container {
    background: rgba(255,255,255,0.2);
    grid-column: 1 / -1;
    margin-top: 20px;
    display: flex;
    flex-direction: row;
  }
  @media (max-width: 600px) {
    
  }
</style>