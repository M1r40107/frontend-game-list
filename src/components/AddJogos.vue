<template>
  <div class="form">
    <h2>Adicionar Jogo</h2>
    <form @submit.prevent="submitForm">
      <label for="nome">Nome do Jogo:</label>
      <input type="text" id="nome" v-model="name" required class="input-field">

      <label for="descricao">Descrição:</label>
      <textarea id="descricao" v-model="description" required class="input-field"></textarea>

      <label for="nota">Avaliação (0 a 10):</label>
      <input type="number" id="nota" v-model.number="rating" min="0" max="10" step="0.1" required class="input-field">

      <label for="preco">Valor:</label>
      <input type="number" id="preco" v-model.number="price" min="0" step="0.01" required class="input-field">

      <button type="submit" class="btn">Adicionar Jogo</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: '',
      description: '',
      rating: 0,
      price: 0,
    };
  },
  methods: {
    submitForm() {
      const newGame = {
        nome: this.name,
        descricao: this.description,
        nota: this.rating,
        preco: this.price,
      };
      this.$emit('add-game', newGame);
      this.name = '';
      this.description = '';
      this.rating = 0;
      this.price = 0;
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
