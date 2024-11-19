<template>
  <div class="form">
    <h2>Deletar Jogo</h2>
    <form @submit.prevent="submitForm">
      <label for="delete-nome">Nome do Jogo:</label>
      <select id="delete-nome" v-model="gameName" required class="input-field">
        <option v-for="game in games" :key="game.nome" :value="game.nome">
          {{ game.nome }}
        </option>
      </select>

      <button type="submit" class="btn">Deletar Jogo</button>
    </form>
  </div>
</template>

<script>
export default {
  props: ['games'],
  data() {
    return {
      gameName: '',
    };
  },
  methods: {
    submitForm() {
      this.$emit('delete-game', this.gameName);
      this.gameName = '';
    },
  },
};
</script>

<style scoped>
.form {
  background-color: #7d4b91;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.input-field {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
  border: none;
  border-radius: 4px;
}

.btn {
  background-color: #ff7f50;
  color: white;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 4px;
  transition: background-color 0.3s ease;
}

.btn:hover {
  background-color: #ff6347;
}
</style>
