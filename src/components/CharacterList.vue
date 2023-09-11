<script setup>
    const character = defineProps(['name', 'id', 'link', 'image', 'species', 'gender', 'status']);

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
    <div class="col-md-12 mb-4">
      <router-link :to="'/character/' + character.id" class="card character-card text-decoration-none">
        <div class="card-body">
          <div class="row">
            <div class="col-md-3">
              <img class="card-img character-image" :src="character.image" alt="Imagem do Personagem">
            </div>
            <div class="col-md-9">
              <h5 class="card-title character-name"><strong>{{ character.name }}</strong></h5>
              <p class="card-text character-species">{{ character.species == "Human" ? "Humano" : character.species }}</p>
              <ul class="list-group list-group-flush">
                <li class="list-group-item character-info">Gênero: {{ getCharacterGender(character.gender) }}</li>
                <li class="list-group-item character-info">Status: {{ getCharacterStatus(character.status) }}</li>
              </ul>
            </div>
          </div>
        </div>
      </router-link>
    </div>
</template>

<style scoped>
    .character-card {
    background-color: #272727;
    border: 1px solid #343434;
    color: #ffffff;
    }

    .character-name {
    font-size: 24px;
    }

    .character-species {
    font-size: 16px;
    }

    .character-info {
    font-weight: bold;
    font-size: 16px;
    }

    .character-image {
    max-width: 100%;
    height: auto;
    }

    .card-clickable {
    cursor: pointer;
    }
</style>