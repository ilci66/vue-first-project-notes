<script setup>
  import WrapperVue from './components/Wrapper.vue';
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="45" height="50" />
    <h1>Digimon Collector</h1>
    <div class="wrapper">
    </div>
  </header>

  <main>
    <WrapperVue />

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
  .container {
    display: flex;
    flex-wrap:wrap;
    justify-items: center;
  }
</style>
