<template>
  <div class="current-digimon-container" @click="isSelected">
    <img class="selected-digimon-img" v-if="selected" :src="selected['0'].img" alt="">
    <p v-if="selected">{{selected["0"].name}}</p>
    <p v-if="selected">{{selected["0"].level}}</p>
  </div>
</template>

<script>
  export default {
    methods: {
      isSelected(){ console.log("is slected", this.selected)}
    },
    props: ["selected"]
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
    margin-top: 10px;
  }
}
.selected-digimon-img{
  height: 200px;
}
</style>