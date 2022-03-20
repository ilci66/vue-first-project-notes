<template>
  <input 
    class="search-digimon" 
    type="text"
    placeholder="Type in the name and hit enter"
    ref="searchbar"
    @change="$emit('searchChange', $event.target.value)"
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
    grid-column: 1 / -1;
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