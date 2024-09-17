<template>
  <div class="form-container">
    <h2>Listado de Empleados</h2>
    <table style="width: 100%;">  
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Edad</th>
          <th>Puesto</th>
          <th>Salario</th>
        </tr>
      </thead>
      <tbody>
    <tr v-for="empleado in empleados" :key="empleado.nombre">
        <td>{{ empleado.nombre }}</td>
        <td>{{ empleado.edad }}</td>
        <td>{{ empleado.puesto }}</td>
        <td>{{ empleado.salario }}</td>
        <td><button @click="eliminarEmpleado(empleado)">Eliminar</button></td>
    </tr>
</tbody>
    </table>
  </div>
</template>

<script>
export default {
  methods: {
    eliminarEmpleado(empleado) {
        this.$emit('eliminar-empleado', empleado);
    }
},
  props: ['empleados'], 
}

</script>

<style>
.form-container {
  padding: 20px;
  border: 1px solid #ccc;
}
</style>
