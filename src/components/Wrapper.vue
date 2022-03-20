<template>
    <div class="wrapper-component">
        <DigimonsListVue />
        <MyCollectionVue />
    </div>
</template>

<script>
import DigimonsListVue from "./DigimonsList.vue"
import MyCollectionVue from "./MyCollection.vue"
    export default {
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