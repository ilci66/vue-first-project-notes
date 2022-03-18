<script setup>
  import allDigimonsVue from './components/allDigimons.vue';
  import MyCollectionVue from './components/MyCollection.vue';
  import DigimonCardVue from './components/DigimonCard.vue';
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="45" height="50" />
    <h1>Digimon Collector</h1>
    <div class="wrapper">
    </div>
  </header>

  <main>
    <allDigimonsVue />
    <!-- <div class="all-digimons">Replace this with all the digimons, can be a div that can be scrolled</div> -->
    
    <MyCollectionVue />
    <!-- <div class="my-collecton">replace it with favourites they will appear as cards, maybe make it look like a deck of cards or something</div> -->

  </main>
</template>

<style>
@import './assets/base.css';
  header{
    display: flex;
    align-items: center;
    justify-content: center;
  }
  h1 {
    font-size: 3rem;
  }

</style>
