<template>
  <div id="app">
    <h1>Rick and Morty Characters</h1>
    <div class="filters">
      <input v-model="name" placeholder="Name" />
      <select v-model="status">
        <option value="">All</option>
        <option value="alive">Alive</option>
        <option value="dead">Dead</option>
        <option value="unknown">Unknown</option>
      </select>
      <button @click="applyFilters">Apply</button>
    </div>
    <div v-if="characters.length" class="characters-list">
      <CharacterCard
        v-for="character in characters"
        :key="character.id"
        :character="character"
      />
    </div>
    <div class="pagination">
      <button @click="prevPage" :disabled="page === 1">Previous</button>
      <button @click="nextPage" :disabled="!info.next">Next</button>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue'
import CharacterCard from './components/CharacterCard.vue'

export default {
  components: {
    CharacterCard,
  },
  setup() {
    const characters = ref([])
    const info = ref({})
    const name = ref('')
    const status = ref('')
    const page = ref(1)

    const fetchCharacters = async () => {
      const response = await fetch(
        `https://rickandmortyapi.com/api/character/?page=${page.value}&name=${name.value}&status=${status.value}`
      )
      const data = await response.json()
      characters.value = data.results
      info.value = data.info
    }

    const applyFilters = () => {
      page.value = 1
      fetchCharacters()
    }

    const nextPage = () => {
      if (info.value.next) {
        page.value++
        fetchCharacters()
      }
    }

    const prevPage = () => {
      if (page.value > 1) {
        page.value--
        fetchCharacters()
      }
    }

    onMounted(() => {
      fetchCharacters()
    })

    return {
      characters,
      info,
      name,
      status,
      page,
      applyFilters,
      nextPage,
      prevPage,
    }
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Permanent+Marker&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

#app {
  text-align: center;
  font-family: 'Roboto', sans-serif;
  background: linear-gradient(120deg, #f6d365 0%, #fda085 100%);
  min-height: 100vh;
  padding: 20px;
}

h1 {
  color: #333;
  font-size: 48px;
  margin-bottom: 30px;
  font-family: 'Permanent Marker', cursive;
}

.filters {
  margin-bottom: 30px;
  display: flex;
  justify-content: center;
  gap: 10px;
}

input,
select {
  padding: 10px;
  border: 2px solid #ddd;
  border-radius: 10px;
  font-size: 16px;
  transition: border-color 0.3s;
  outline: none;
}

input:focus,
select:focus {
  border-color: #ff7e5f;
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 10px;
  background-color: #ff7e5f;
  color: white;
  font-size: 16px;
  cursor: pointer;
  transition: background-color 0.3s, transform 0.3s;
  font-family: 'Roboto', sans-serif;
}

button:hover {
  background-color: #ea6b4d;
  transform: scale(1.05);
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

.characters-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.pagination {
  margin-top: 30px;
  display: flex;
  justify-content: center;
  gap: 10px;
}

.pagination button {
  margin: 0 10px;
}
</style>
