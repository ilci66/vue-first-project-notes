<template>
  <SearchVue @searchChange="handleSearch" />
  <div class="digimons-list-container" v-if="filteredDigimons === undefined" >
    <p 
      @click="handleDigimonClick" 
      class="digimons-list" 
      v-for="digimon in allDigimons" :key="digimon.name"
      :id="digimon.name"
    >
      <i style="font-size: .9rem"> Name:</i> <b>{{digimon.name}}</b> ---- <i style="font-size: .9rem">Level:</i> {{digimon.level}}
      <button @click="$emit('add', 'a')">asdasd</button>  
    </p>
  </div> 
  <div class="digimons-list-container" v-if="filteredDigimons" >
    <p 
      @click="handleDigimonClick" 
      class="digimons-list" 
      v-for="digimon in filteredDigimons" :key="digimon.name"
      :id="digimon.name"
    >
      <i style="font-size: .9rem"> Name:</i> <b>{{digimon.name}}</b> ---- <i style="font-size: .9rem">Level:</i> {{digimon.level}}
      <button @click="$emit('add', 'a')">asdasd</button>  
    </p>
  </div> 
  <div class="digimons-list-container" v-if="filteredDigimons" >
    <p 
      @click="handleDigimonClick" 
      class="digimons-list" 
      v-for="digimon in filteredDigimons" :key="digimon.name"
      :id="digimon.name"
    >
      <i style="font-size: .9rem"> Name:</i> <b>{{digimon.name}}</b> ---- <i style="font-size: .9rem">Level:</i> {{digimon.level}}
      <button @click="$emit('add', 'a')">asdasd</button>  
    </p>
  </div>
  <CurrentDigimonVue :selected="this.selected" />
</template>

<script>
  import SearchVue from './Search.vue'
  import CurrentDigimonVue from './CurrentDigimon.vue'

  export default {
    methods: {
      handleFetchAll(){
        fetch('https://digimon-api.herokuapp.com/api/digimon')
          .then(res => res.json())
          .then(data => {
            this.allDigimons = data; 
            console.log(data)
            this.filteredDigimons = undefined;
          })
      },
      handleDigimonClick(event){
        this.selected = this.allDigimons.filter(ele => ele.name === event.target.id)
      },
      handleSearch(event){
        console.log("logging evet",event)
        this.filteredDigimons = this.allDigimons.filter(d => d.name === event)
      }
    },
    props:["add"],
    components: {
      SearchVue,
      CurrentDigimonVue
    },
    data() {
      return {
        allDigimons: [],
        filteredDigimons: undefined,
        selected: undefined,
      }
    },
    emits: ["testingEmit"],
    mounted() {
      // fetch('https://digimon-api.herokuapp.com/api/digimon')
      // .then(res => res.json())
      // .then(data => {
      //   this.allDigimons = data; 
      //   console.log(data)
      // })
      this.handleFetchAll()
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
    overflow: scroll;
    overflow-x :hidden;
    background: rgba(29, 15, 15, 0.4);
    display: flex;
    flex-direction: column;
  }
  @media (max-width: 600px){
    .digimons-list-container{
      grid-column: 1 / -1;
    }
  };
</style>