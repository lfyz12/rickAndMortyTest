<template>
  <div>
    <div>
      <input v-model="filters.name" placeholder="Name" style="margin-right: 10px"/>
      <select v-model="filters.status" style="margin-right: 10px">
        <option value="">All</option>
        <option value="alive">Alive</option>
        <option value="dead">Dead</option>
        <option value="unknown">Unknown</option>
      </select>
      <button @click="applyFilters">Найти</button>
    </div>
    <div class="char-list">
      <CharacterCard v-for="character in characters" :key="character.id" :character="character" />
    </div>
    <div style="margin-top: 20px; margin-left: 20px">
      <button @click="prevPage" :disabled="page === 1">Previous</button>
      <span>Page {{ page }}</span>
      <button @click="nextPage" :disabled="!hasMore">Next</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import CharacterCard from './CharacterCard.vue';
import { ref } from 'vue';

export default {
  name: 'CharacterList',
  components: {
    CharacterCard
  },
  setup() {
    const characters = ref([]);
    const page = ref(1);
    const hasMore = ref(true);
    const filters = ref({
      name: '',
      status: ''
    });

    const fetchCharacters = async () => {
      const { data } = await axios.get('https://rickandmortyapi.com/api/character', {
        params: {
          page: page.value,
          name: filters.value.name,
          status: filters.value.status
        }
      });
      characters.value = data.results;
      hasMore.value = data.info.next !== null;
    };

    const applyFilters = () => {
      page.value = 1;
      fetchCharacters();
    };

    const nextPage = () => {
      page.value += 1;
      fetchCharacters();
    };

    const prevPage = () => {
      page.value -= 1;
      fetchCharacters();
    };

    fetchCharacters();

    return {
      characters,
      page,
      hasMore,
      filters,
      applyFilters,
      nextPage,
      prevPage
    };
  }
}
</script>

<style>
.char-list {
  width: 98vw;
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  background: #4d4d4d;
  margin-top: 20px;
}
</style>