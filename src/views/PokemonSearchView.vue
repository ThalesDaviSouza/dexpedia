<template>
    <main>
        <DexSearch
            :endpoint="'https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0'"
            @search="res => console.log(res)"
        >
            Pokemon
        </DexSearch>
    </main>
</template>

<script setup>
import DexSearch from '../components/DexSearch.vue'
</script>

<style scoped>

</style>