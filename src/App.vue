<template>
  <div>
    <h1>Gestiónador de Tareas</h1>

    <!-- Formulario para agregar o editar tareas -->

     <!--A continuacion veremos los eventos y props para la comunicacion entre componentes -->
    <TareaForm 
      @nueva-tarea="agregarTarea" 
      :tarea-editada="tareaSeleccionada" 
      @actualizar-tarea="actualizarTarea" 
    />
 
    <!-- Tabla de Tareas con Botones -->
    <v-container fluid class="table-container">
      <v-table theme="dark" class="ma-4 full-width-table" fixed-header>
        <thead>
          <tr>
            <!--Aqui se crea la tabla-->
            <th class="text-left column-name">Nombre de la Tarea</th>
            <th class="text-left column-state">Estado</th>
            <th class="text-left column-accion">Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(tarea, index) in tareas" :key="index"> <!--Este v-for lo que hace es colocar la informacion en la tabla -->
            <td>{{ tarea.nombre }}</td>
            <td>{{ tarea.estado }}</td>
            <td class="action-buttons">
              <v-btn color="success" @click="seleccionarTarea(index)">Editar</v-btn>
              <v-btn color="error" @click="eliminarTarea(index)">Eliminar</v-btn>
            </td>
          </tr>
        </tbody>
      </v-table>
    </v-container>
  </div>
</template>

<script>
//Aqui se importa el componente 
import TareaForm from './components/TareaForm.vue';
import { ref } from 'vue';

//
export default {
  name: 'App',
  components: {
    TareaForm,
  },
  setup() {
    //definimos una lista reactiva para las tareas
    const tareas = ref([]);
    //Tarea seleccionada para la edicion 
    const tareaSeleccionada = ref(null);

    //funcion para agregar una nueva tarea
    const agregarTarea = (nuevaTarea) => {
      tareas.value.push(nuevaTarea);
    };

    //funcion para eliminar la tarea
    const eliminarTarea = (index) => {
      tareas.value.splice(index, 1);
    };

    //Funcion para seleccionar una tarea y despues editarla
    const seleccionarTarea = (index) => {
      tareaSeleccionada.value = { ...tareas.value[index], index };
    };

    //funcion para actulizar una tarea ya agregada
    const actualizarTarea = (tareaActualizada) => {
      if (tareaActualizada.index !== undefined) {
        tareas.value[tareaActualizada.index] = {
          nombre: tareaActualizada.nombre,
          estado: tareaActualizada.estado,
        };
      }
      tareaSeleccionada.value = null;
    };

    return {
      tareas, //exportamos la lista de tareas
      agregarTarea, //Funcion para agregar tarea
      eliminarTarea, //Funcion para eliminar tarea
      seleccionarTarea, //Funcion para seleccionar tareas a editar
      actualizarTarea, //Funcion para actualizar tareas
      tareaSeleccionada, //Exportar la tarea seleccionada para edicion 
    };
  },
};
</script>

<style scoped>
.table-container {
  width: 100%;
  height: 65vh; /* Esto asegura que ocupe el 100% de la altura del viewport */
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

.full-width-table {
  width: 100% !important; /* Asegura que la tabla ocupe todo el ancho disponible */
  flex-grow: 1; /* Permite que la tabla se expanda para llenar el espacio restante */
}

.column-name,
.column-state,
.column-accion {
  width: 33%; /* Distribuye el ancho de manera equitativa entre las tres columnas */
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}

.action-buttons {
  display: flex;
  gap: 10px; /* Espacio entre los botones */
  justify-content: space-evenly; /* Espacia los botones de manera uniforme */
}
</style>
