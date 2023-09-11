<script setup>
import { onMounted, reactive, ref } from 'vue';
import CharacterList from '../components/CharacterList.vue'

let people = reactive(ref([]));
let currentPage = ref(1);

onMounted(() => {
  fetchCharacters();
});

const fetchCharacters = () => {
  fetch(`https://rickandmortyapi.com/api/character/?page=${currentPage.value}`)
    .then(res => res.json())
    .then(res => {
      people.value = res.results;
    });
};

const nextPage = () => {
  currentPage.value++;
  fetchCharacters();
};

const previousPage = () => {
  if (currentPage.value > 1) {
    currentPage.value--;
    fetchCharacters();
  }
};

</script>

<template>
  <main>
    <div class="container mb-70">
      <div class="row mt-4">
        <div class="col-md-12">
          <div class="card-deck">
            <CharacterList
              v-for="person in people"
              :key="person.id"
              :id="person.id"
              :name="person.name"
              :link="person.url"
              :image="person.image"
              :gender="person.gender"
              :status="person.status"
              :species="person.species"
            />
          </div>
        </div>
      </div>

       <div class="row mt-4">
        <div class="col-md-12 text-center">
          <nav aria-label="Page navigation">
            <ul class="pagination justify-content-center">
              <li class="page-item" :class="{ disabled: currentPage === 1 }">
                <button class="page-link" @click="previousPage" :disabled="currentPage === 1">Anterior</button>
              </li>
              <li class="page-item" :class="{ disabled: currentPage === totalPages }">
                <button class="page-link" @click="nextPage" :disabled="currentPage === totalPages">Próxima</button>
              </li>
            </ul>
          </nav>
        </div>
      </div>
    </div>
  </main>
</template>
