<!-- TODO: Fazer esse componente ser respansivo -->
<template>
    <h1>
        <slot></slot>
    </h1>
    <section class="wrapper">
        <div class="search-wrapper">
            <div class="search">
                <input type="text" v-model="searchOptions.search">
                <button @click="search">
                    <Icon icon="tabler:search" />
                </button>
            </div>
            <div>
                <span v-if="searchOptions.response" class="search-count">{{ searchOptions.resultsCount }} resultados para "{{ searchOptions.searchDisplay }}"</span>
                <div class="search-options">
                    <div>
                        <span>Ordenar por </span>
                        <select>
                            <option value="a-z">A-Z</option>
                            <option value="z-a">Z-A</option>
                        </select>
                    </div>
                    <div>
                        <span>Mostrando por página </span>
                        <select v-model="searchOptions.maxResults">
                            <option value="20">20</option>
                            <option value="40">40</option>
                            <option value="60">60</option>
                        </select>
                    </div>
                    <div class="choose-page">
                        <Icon icon="mingcute:left-fill" />
                        <span>1</span>
                        <Icon icon="mingcute:right-fill" />
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { Icon } from '@iconify/vue';
import { reactive } from 'vue';

const emit = defineEmits(['search']);

const props = defineProps({
    endpoint: {
        type: String,
        required: true
    }
})

const searchOptions = reactive({
    search: '',
    maxResults: 20,
    resultsCount: '',
    searchDisplay: '',
    response: null
})

const search = () => {
    fetch(props.endpoint)
    .then(res => res.json())
    .then(res => {
        res.results = res.results.filter(poke => poke.name.includes(searchOptions.search));
        
        searchOptions.resultsCount = res.results.length;
        searchOptions.searchDisplay = searchOptions.search;
        res.results = res.results.slice(0, searchOptions.maxResults);
        searchOptions.response = res.results;

        return res.results;
    })
    .then(res => emit('search', res))
};

</script>

<style scoped>
.search {
    display: flex;
    flex-direction: row;
    width: 70%;
    align-items: center;
}
.search>*{
    font-size: 18px;
    padding: 4px 8px;
}
.search>input{
    width: 80%;
}

.search-count{
    padding: 5px;
}

.search-options {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    padding: 5px;
}

.choose-page{
    display: flex;
    align-items: center;
}
</style>