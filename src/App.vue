<template>
  <div class="container">
    <h1>Gestión de Empleados</h1>
    <div id="menu">
      <button @click="showForm('agregar')">Agregar Empleado</button>
      <button @click="showForm('actualizar')">Actualizar Puesto</button>
      <button @click="listarEmpleados()">Listar Empleados</button>
    </div>
    <div class="content">
      <div class="form-section">
        <AgregarEmpleado v-if="showFormType === 'agregar'" @agregar-empleado="agregarEmpleado" />
        <ActualizarPuesto
          v-if="showFormType === 'actualizar'"
          @actualizar-puesto="actualizarPuesto"
        />
      </div>
      <div class="table-section" v-if="showListado">
        <ListarEmpleados :empleados="empleados" @eliminar-empleado="eliminarEmpleado" />
      </div>
    </div>
    <div v-if="error" class="error">{{ error }}</div>
    <div v-if="errorActualizar" class="error">{{ errorActualizar }}</div>
  </div>
</template>

<script>
import AgregarEmpleado from './components/AgregarEmpleado.vue'
import ActualizarPuesto from './components/ActualizarPuesto.vue'
import ListarEmpleados from './components/ListarEmpleados.vue'

export default {
  components: {
    AgregarEmpleado,
    ActualizarPuesto,
    ListarEmpleados
  },
  data() {
    return {
      showFormType: null,
      showListado: false,
      empleados: [],
      error: null,
      errorActualizar: null,
      errorEliminar: null
    }
  },
  methods: {
    showForm(type) {
      this.showFormType = type
      this.showListado = true
      this.error = null
      this.errorActualizar = null
      this.errorEliminar = null
    },
    agregarEmpleado(nuevoEmpleado) {
      if (this.empleados.some((e) => e.puesto === nuevoEmpleado.puesto)) {
        this.error = 'El número de puesto ya está en uso'
      } else {
        this.empleados.push(nuevoEmpleado)
        this.error = null
      }
    },
    actualizarPuesto({ nombre, nuevoPuesto }) {
      const empleado = this.empleados.find((e) => e.nombre === nombre);
      if (!empleado) {
        this.errorActualizar = 'Empleado no encontrado';
      } else if (this.empleados.some(e => e.puesto === nuevoPuesto)) {
        this.errorActualizar = 'El número de puesto ya está en uso';
      }  
      else {
        empleado.puesto = nuevoPuesto;
        this.errorActualizar = '';
      }
    },
    eliminarEmpleado(empleadoAEliminar) {
      const index = this.empleados.findIndex((empleado) => empleado === empleadoAEliminar)
      if (index !== -1) {
        this.empleados.splice(index, 1)
        this.errorEliminar = null
      }
    },
    listarEmpleados() {
      this.showFormType = null
      this.showListado = true
      this.errorActualizar = ''
    }
  }
}
</script>

<style>
body {
  background-color: #121212;
  color: #e0e0e0;
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}
.container {
  margin: 0 auto;
  padding: 20px;
}
h1 {
  text-align: center;
  color: #1e88e5;
}
#menu {
  text-align: center;
  margin-bottom: 20px;
}
#menu button {
  margin: 5px;
  padding: 10px 20px;
  background-color: #1e88e5;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}
#menu button:hover {
  background-color: #1565c0;
}
.content {
  flex: 1;
  width: max-content;
  display: flex;
  justify-content: space-between;
}
.form-section,
.table-section {
  width: 48%;
}
.form-container {
  padding: 20px;
  border: 1px solid #333;
  border-radius: 5px;
  background-color: #1e1e1e;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
}
.error {
  color: red;
  margin-top: 5px;
}
table {
  width: 100%;
  border-collapse: collapse;
  background-color: #1e1e1e;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.5);
  overflow-x: auto;
  overflow-y: auto;
}
table,
th,
td {
  border: 1px solid #333;
}
th,
td {
  padding: 10px;
  text-align: left;
  white-space: nowrap;
}
th {
  background-color: #333;
}
tr:nth-child(even) {
  background-color: #2e2e2e;
}
button.eliminar {
  background-color: #dc3545;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  padding: 5px 10px;
  transition: background-color 0.3s;
}
button.eliminar:hover {
  background-color: #c82333;
}
</style>
