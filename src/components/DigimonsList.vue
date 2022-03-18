<template>
  <SearchVue />
  <div class="digimons-list-container">
    <ul>
      <li class="digimons-list" v-for="digimon in allDigimons" :key="digimon.name">Name: {{digimon.name}}, Level: {{digimon.level}}</li>
    </ul>
  </div> 
</template>

<script>
  import SearchVue from './Search.vue'

  export default {
    components: {
      SearchVue
    },
    data() {
      return {
        allDigimons: []
      }
    },
    mounted() {
      fetch('https://digimon-api.herokuapp.com/api/digimon')
      .then(res => res.json())
      .then(data => {
        this.allDigimons = data; 
        console.log(data)
      })

    }
  }
</script>

<style scoped>
  .digimons-list{
    margin: 0;
    padding: 0;
    list-style:none;
    color: rgb(0, 0, 0);
    font-size: 1.2rem;

  }

  .digimons-list-container {
    max-height: 300px;
    max-width: 600px;
    overflow: scroll;
    overflow-x :hidden;
    background: rgb(236, 210, 228);
    margin: 0 auto;
  }
</style>