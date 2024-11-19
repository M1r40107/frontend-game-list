<template>
  <div class="container">
    <header class="header">
      <h1 class="header_name">CEBOLINHAS CABEÇUDO GAMES</h1>
      <p>MELHORES JOGOS</p>
    </header>

    <div class="body">
      <add-jogos @add-game="addGame"></add-jogos>
      <delete-jogos :games="games" @delete-game="deleteGame"></delete-jogos>

      <div class="game-list">
        <div class="game-item" v-for="(game, index) in games" :key="index">
          <h2>{{ game.nome }}</h2>
          <p class="description">{{ game.descricao }}</p>
          <p class="rating">Avaliação: {{ game.nota }}/10</p>
          <p class="price">Valor: R$ {{ game.preco.toFixed(2) }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import AddJogos from './components/AddJogos.vue';
import DeleteJogos from './components/DeleteJogos.vue';

export default {
  components: {
    AddJogos,
    DeleteJogos,
  },
  data() {
    return {
      games: [
        { nome: 'The Legend of Zelda: Breath of the Wild', descricao: 'Ação/Aventura', preco: 220.99, nota: 9.8 },
        { nome: 'God of War', descricao: 'Ação/Aventura', preco: 149.99, nota: 9.7 },
        { nome: 'The Witcher 3: Wild Hunt', descricao: 'RPG', preco: 144.99, nota: 9.6 },
        { nome: 'Red Dead Redemption 2', descricao: 'Ação/Aventura', preco: 159.99, nota: 9.7 },
        { nome: 'Sekiro: Shadows Die Twice', descricao: 'Ação/Aventura', preco: 200.99, nota: 9.5 },
      ],
    };
  },
  methods: {
    async fetchGames() {
      try {
        const response = await axios.get('http://localhost:8080/games');
        this.games = response.data;
      } catch (error) {
        console.error('Erro ao buscar jogos:', error);
      }
    },
    async addGame(newGame) {
      try {
        const response = await axios.post('http://localhost:8080/addgame', newGame);
        this.games.push(response.data);
      } catch (error) {
        console.error('Erro ao adicionar jogo:', error);
      }
    },
    async deleteGame(gameName) {
      try {
        await axios.delete('http://localhost:8080/deletegames', { data: { nome: gameName } });
        this.games = this.games.filter(game => game.nome !== gameName);
      } catch (error) {
        console.error('Erro ao deletar jogo:', error);
      }
    },
  },
  created() {
    this.fetchGames();
  },
};
</script>

<style scoped>
.container {
  background-color: #511e6e;
  color: white;
  min-height: 100vh;
  font-family: Arial, sans-serif;
  padding: 20px;
}

.header {
  text-align: center;
  margin-bottom: 20px;
}

.header_name {
  font-size: 28px;
  font-weight: bold;
  color: orange;
  margin-bottom: 5px;
}

.body {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.game-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
}

.game-item {
  background-color: #693c7e;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.game-item h2 {
  font-size: 18px;
  margin-bottom: 5px;
}

.description {
  font-size: 14px;
  margin-bottom: 3px;
}

.rating, .price {
  font-size: 14px;
}
</style>
