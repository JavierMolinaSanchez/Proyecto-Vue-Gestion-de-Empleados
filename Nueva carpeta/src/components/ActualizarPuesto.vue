<template>
  <div class="form-container">
    <h2>Actualizar Puesto</h2>
    <form @submit.prevent="actualizarPuesto">
      <div>
        <label for="nombreActualizar">Nombre:</label>
        <input type="text" id="nombreActualizar" v-model="nombreActualizar" required />
      </div>
      <div>
        <label for="nuevoPuesto">Nuevo Puesto:</label>
        <input type="number" id="nuevoPuesto" v-model.number="nuevoPuesto" required min="1" />
      </div>
      <button type="submit">Actualizar</button>
    </form>
    <div v-if="errorActualizar" class="error">{{ errorActualizar }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombreActualizar: '',
      nuevoPuesto: null,
      errorActualizar: null,
    };
  },
  methods: {
    actualizarPuesto() {
      // Emitir el evento para actualizar el puesto
      this.$emit('actualizar-puesto', {
        nombre: this.nombreActualizar,
        nuevoPuesto: this.nuevoPuesto,
      });

      // Limpiar los campos y errores
      this.nombreActualizar = '';
      this.nuevoPuesto = null;
      this.errorActualizar = null;
    },
  },
};
</script>


<style>
.form-container {
  margin-bottom: 20px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #f9f9f9;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.error {
  color: red;
  margin-top: 5px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #0056b3;
}
</style>
