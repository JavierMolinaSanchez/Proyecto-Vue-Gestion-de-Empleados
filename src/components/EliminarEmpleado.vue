<template>
    <div class="form-container">
      <h2>Eliminar Empleado</h2>
      <form @submit.prevent="eliminarEmpleado">
        <div>
          <label for="nombreEliminar">Nombre:</label>
          <input type="text" id="nombreEliminar" v-model="nombreEliminar" required />
        </div>
        <button type="submit">Eliminar</button>
      </form>
      <div v-if="errorEliminar" class="error">{{ errorEliminar }}</div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        nombreEliminar: '',
        errorEliminar: null,
      };
    },
    methods: {
      eliminarEmpleado() {
        this.$emit('eliminar-empleado', this.nombreEliminar);
        this.nombreEliminar = '';
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
  
  