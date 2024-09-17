<template>
  <div class="form-container">
    <h2>Agregar Empleado</h2>
    <form @submit.prevent="agregarEmpleado">
      <div>
        <label for="nombre">Nombre:</label>
        <input
          type="text"
          id="nombre"
          v-model="nombre"
          required
          @input="validarNombre"
        />
        <p v-if="!nombreValido && nombre.trim() !== ''" class="error">
          El nombre solo puede contener letras.
        </p>
      </div>
      <div>
        <label for="edad">Edad:</label>
        <input type="number" id="edad" v-model.number="edad" required min="1" />
      </div>
      <div>
        <label for="puesto">Puesto:</label>
        <input type="text" id="puesto" v-model="puesto" required />
      </div>
      <div>
        <label for="salario">Salario:</label>
        <input
          type="number"
          id="salario"
          v-model.number="salario"
          required
          step="0.01"
          min="1"
        />
      </div>
      <button type="submit" id="btnAgregar">Agregar</button>
      <button type="reset" id="btnLimpiar">Limpiar Campos</button>
    </form>
    <div v-if="error" class="error">{{ error }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombre: "",
      edad: null,
      puesto: null,
      salario: null,
      error: null,
      nombreValido: true,
    };
  },
  methods: {
    validarNombre() {
      this.nombreValido =
        this.nombre.trim() !== "" &&
        /^[a-zA-ZáéíóúüñÁÉÍÓÚÜÑ]+$/.test(this.nombre);
      // Oculta el mensaje de error si el nombre es válido
      if (this.nombreValido) {
        this.error = null; // Limpia el mensaje de error
      }
    },
    agregarEmpleado() {
      if (this.nombre.trim() !== "" && !this.nombreValido) {
        this.error = "El nombre no es válido.";
        return;
      }

      this.$emit("agregar-empleado", {
        nombre: this.nombre,
        edad: this.edad,
        puesto: this.puesto,
        salario: this.salario,
      });

      this.nombre = "";
      this.edad = null;
      this.puesto = null;
      this.salario = null;
      this.error = null;
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

#btnAgregar, #btnLimpiar{
  display: flex 1;
  justify-content: space-around;
  
}


button:hover {
  background-color: #0056b3;
}
</style>
