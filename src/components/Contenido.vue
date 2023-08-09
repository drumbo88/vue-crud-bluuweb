<template>
  <div class="container mt-5">
    <h3>{{ titulo }}</h3>

    <input
      type="text"
      class="form-control my-3"
      v-model="nuevaTarea"
      @keyup.enter="agregarTarea"
    />
    <button @click="agregarTarea" class="btn btn-primary">Agregar</button>

    <div class="mt-3" v-for="(item, index) of tareas" v-bind:key="index">
      <div :class="['alert', item.estado ? 'alert-success' : 'alert-danger']" role="alert">
        <div class="d-flex justify-content-between align-items-center">
          <div>{{ index }} - {{ item.nombre }} - {{ item.estado }}</div>
          <div>
            <button class="btn btn-success btn-sm" @click="editarTarea(index)">OK</button>
            <button class="btn btn-danger btn-sm" @click="eliminarTarea(index)">X</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Contenido",
  data() {
    return {
      titulo: "GYM con Vue",
      tareas: [],
      nuevaTarea: ""
    };
  },
  methods: {
    // No usar funciones de flecha
    agregarTarea() {
      const nuevaTarea = this.nuevaTarea.trim();
      if (!nuevaTarea) return;
      this.tareas.push({
        nombre: nuevaTarea,
        estado: false
      });
      this.nuevaTarea = "";
      this.guardarTareas(this.tareas)
    },
    editarTarea(index) {
        this.tareas[index].estado = true
        this.guardarTareas(this.tareas)
    },
    eliminarTarea(index) {
        this.tareas.splice(index, 1)
        this.guardarTareas(this.tareas)
    },
    guardarTareas(tareas) {
        localStorage.setItem('gym', JSON.stringify(tareas))
    }
  },
  created() {
    let datosDB = JSON.parse(localStorage.getItem('gym'))
    this.tareas = (datosDB === null) ? [] : datosDB
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
</style>
