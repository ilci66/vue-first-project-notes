<template>
  <SearchVue />
  <div class="digimons-list-container">
      <p 
        @click="handleDigimonClick" 
        class="digimons-list" 
        v-for="digimon in allDigimons" :key="digimon.name"
        :id="digimon.name"
      >
        <i style="font-size: .9rem"> Name:</i> <b>{{digimon.name}}</b> ---- <i style="font-size: .9rem">Level:</i> {{digimon.level}}
      </p>
  </div> 
  <CurrentDigimonVue :selected="this.selected" />
</template>

<script>
  import SearchVue from './Search.vue'
  import CurrentDigimonVue from './CurrentDigimon.vue'

  export default {
    methods: {
      handleDigimonClick(event){
        this.selected = this.allDigimons.filter(ele => ele.name === event.target.id)
      }
    },
    components: {
      SearchVue,
      CurrentDigimonVue
    },
    data() {
      return {
        allDigimons: [],
        selected: undefined,
      }
    },
    emits: ["testingEmit"],
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
    color: rgb(255, 255, 255);
    font-size: 1.2rem;
    width: 100%;
    text-align: center;
  }
  .digimons-list:hover {
    background: rgba(0,0,0,.25); 
    cursor: pointer;
  }

  .digimons-list-container {
    max-height: 300px;
    width: 60%;
    overflow: scroll;
    overflow-x :hidden;
    background: rgba(29, 15, 15, 0.4);
    margin: 0 auto;
    display: flex;
    flex-direction: column;
  }
  @media (max-width: 600px){
    .digimons-list-container{
      width: 100%;
    }
  };
</style>