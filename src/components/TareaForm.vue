<template>
    <div>
      <!--Formulario para crear o actualizar una tarea-->
      <v-form @submit.prevent="procesarFormulario">
      <!--Campo de texto para el nombre de la tarea-->
      <!--asignacion de la variable donde se va a guardar y requisitos y pruebas para campos requeridos-->
        <v-text-field
          v-model="tarea.nombre"
          label="Nombre de la Tarea"
          :rules="[rules.requerido]"
          required 
        ></v-text-field>
        <!--Selector de estado de la tarea-->
        <!--Se guarda segun el estado en la variable y se hacen los requisitos y pruebas para campo obligatorio -->
        <v-select
          v-model="tarea.estado"
          :items="['Pendiente', 'Completada']"
          label="Estado"
          :rules="[rules.requerido]"
          required
        ></v-select>
        <!--Boton para enviar el formulario-->
        <v-btn type="submit" color="primary">
          {{ tarea.index !== undefined ? 'Actualizar' : 'Aceptar' }}
        </v-btn>
      </v-form>
    </div>
  </template>
  
  <script>
  import { ref, watch } from 'vue';
  
  export default {
    name: 'TareaForm',
    props: {
      tareaEditada: {
        type: Object, //se recibe la tarea editada del componente App.vue
        default: null,
      },
    },
    emits: ['nueva-tarea', 'actualizar-tarea'],//Estos eventos son los que vamos a emitir hacia el componente padre 
    setup(props, { emit }) {
      //creamos una variable reactiva para los datos del formulario
      const tarea = ref({ nombre: '', estado: '', index: undefined });
      //Reglas para la validacion de campo requerido
      const rules = {
        requerido: (v) => !!v || 'Este campo es obligatorio',
      };
  
      // Cargar los datos de la tarea a editar
      watch(
        () => props.tareaEditada,
        (nuevaTarea) => {
          if (nuevaTarea) {
            tarea.value = { ...nuevaTarea }; //si hay una tarea para editar, cargamos sus datos
          } else {
            tarea.value = { nombre: '', estado: '', index: undefined }; //de lo contrario limpiamos el formulario
          }
        },
        { immediate: true }//Esta linea sirve para ejecutar de inmediato cuando se carga el componente
      );
  
      //Esta funcion se ejecuta cuando el usuario envia el formulario 
      const procesarFormulario = () => {
        // Verificamos que ambos campos tengan algún valor antes de proceder
        if (!tarea.value.nombre || !tarea.value.estado) {
        // Si alguno de los campos está vacío, mostramos un mensaje o no hacemos nada
            alert('Por favor, complete todos los campos antes de enviar.');
            return; // Evita que se emita el evento si los campos están vacíos
        }
        
        //si contiene el index quiere decir que estamos actualizando una tarea ya existente 
        if (tarea.value.index !== undefined) {
          emit('actualizar-tarea', { ...tarea.value });//emitimos el evento para actualizar la tarea 
        } else {
          emit('nueva-tarea', { nombre: tarea.value.nombre, estado: tarea.value.estado });// de lo contrario emitimos para crear una nueva tarea 
        }
        //Limpia el formulario despues de enviar
        tarea.value = { nombre: '', estado: '', index: undefined }; // Resetear el formulario
      };
  
      return {
        tarea, //retorna los datos reactivos 
        rules, //Retorna las reglas de validacion 
        procesarFormulario, //Retorna la funcion para procesar el formulario
      };
    },
  };
  </script>
  
  <style scoped>
  
  </style>
  