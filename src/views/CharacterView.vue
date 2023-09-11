<script setup>
  import { onMounted, reactive, ref } from 'vue';
  import { useRoute, useRouter } from 'vue-router';

  const character = reactive(ref([]));

  const route = useRoute();
  const characterId = ref(route.params.id);

  const router = useRouter();

  const goBack = () => {
    router.back();
  };

  onMounted(() => {
    fetchCharacter();
  });

  const fetchCharacter = () => {
    fetch(`https://rickandmortyapi.com/api/character/${characterId.value}`)
      .then(res => res.json())
      .then(data => {
        character.value = data;
        console.log(character.value);
      })
      .catch(error => {
        console.error(error);
      });
  };

  // Mapeamento de status e gênero
  const statusMapping = {
    'Dead': 'Morto',
    'Alive': 'Vivo',
  };

  const genderMapping = {
    'Female': 'Feminino',
    'Male': 'Masculino',
    'Genderless': 'Sem gênero',
  };

  // Funções para obter os valores mapeados. Coloquei um retorno padrão caso não esteja no meu mapeamento
  const getCharacterStatus = (status) => {
    return statusMapping[status] || 'Desconhecido';
  };

  const getCharacterGender = (gender) => {
    return genderMapping[gender] || 'Desconhecido';
  };
</script>

<template>
  <div class="container mt-4">
    <div class="row">
      <div class="col-md-12">
        <button @click="goBack" class="btn btn-primary mb-3">Voltar</button>
        
        <h2>Detalhes do Personagem</h2>
        
        <div class="card bg-dark text-white">
          <div class="row no-gutters">
            <div class="col-md-4">
              <img class="card-img" :src="character.image" alt="Imagem do Personagem">
            </div>
            <div class="col-md-8">
              <div class="card-body">
                <h5 class="card-title text-capitalize"><strong>{{ character.name }}</strong></h5>
                <ul class="list-group list-group-flush">
                  <li class="list-group-item">
                    <strong>Status:</strong> {{ getCharacterStatus(character.status) }}
                  </li>
                  <li class="list-group-item">
                    <strong>Espécie:</strong> {{ character.species }}
                  </li>
                  <li class="list-group-item">
                    <strong>Gênero:</strong> {{ getCharacterGender(character.gender) }}
                  </li>
                  <li class="list-group-item" v-if="character.origin">
                    <strong>Origem:</strong> {{ character.origin.name }}
                  </li>
                  <li class="list-group-item" v-if="character.location">
                    <strong>Localização:</strong> {{ character.location.name }}
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
  body {
    background-color: #1f1f1f;
    color: #ffffff;
  }

  .card {
    background-color: #272727;
    border: 1px solid #343434;
  }

  .card-title {
    font-size: 24px;
    color: #ffffff; /* Cor do título */
  }

  .list-group-item {
    background-color: #1f1f1f;
    border: none;
    font-size: 16px;
    color: #ffffff;
  }

  .btn-primary {
    background-color: #6ea04b;
    border-color: #6ea04b;
  }

  .btn-primary:hover {
    background-color: #55893b;
    border-color: #55893b;
  }

  .btn-primary:focus {
    background-color: #55893b;
    border-color: #55893b;
  }
</style>