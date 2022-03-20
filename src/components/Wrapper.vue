<template>
    <div class="wrapper-component">
        <DigimonsListVue @add-to-list="addToList"/>
        <MyCollectionVue :collection="this.collection" />
    </div>
</template>

<script>
import DigimonsListVue from "./DigimonsList.vue"
import MyCollectionVue from "./MyCollection.vue"
  export default {
    data(){
      return {
        collection: []
      }
    },
    methods:{
      addToList(obj){
        console.log("to add ==>", obj)
        if(this.collection.length < 5 ) {
          this.collection = [...this.collection, obj];
          console.log("cllection",this.collection)
        }
      
      }
    },
    components: {
      DigimonsListVue,
      MyCollectionVue
    },
  }
</script>

<style scoped>
    .wrapper-component{
        display: grid;
        grid-template-columns: 2fr 1fr;
        grid-gap:40px;
        align-items: center;
        justify-content: space-around;
        max-width: 960px;
        margin: 0 auto;
    }
    @media (max-width: 600px) {
    }
</style>