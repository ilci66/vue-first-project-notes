<template>
  <input 
    class="search-digimon" 
    type="text"
    placeholder="Search any digimon by name"
    ref="searchbar"
    >
</template>

<script>
  export default {
    mounted(){
    }
  }
</script>

<style scoped>
  .search-digimon {
    width: 100%;
    padding: 10px 5px;
    border: none;
    box-shadow: 0 0 8px white;
    margin-bottom: 10px;
    text-align: center;
    font-size: 2rem;
  }
  .search-digimon :focus {
    box-shadow: 0 0 16px white;
  }
</style>