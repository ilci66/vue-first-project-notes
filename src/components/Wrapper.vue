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
        grid-template-columns: 5fr 2fr;
        grid-gap:30px;
        align-items: center;
        justify-content: space-around;
    }
    @media (max-width: 600px) {
    }
</style>