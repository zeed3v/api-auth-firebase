<template>
<h1 class="my-5">Formularios con Vue.js</h1>
  <form @submit.prevent="procesarformulario">
    <Input :tarea="tarea"/>
    
  </form>
  <hr>
  <ListaTareas />
</template>

<script>
import Input from '../components/Input.vue'
import ListaTareas from '../components/ListaTareas.vue'
import {mapActions} from 'vuex'
const shortid = require('shortid');

export default {
  name: 'HomeView',
  components: {
    Input, ListaTareas
  },
  data(){
    return{
      tarea:{
        id: '',
        nombre:'',
        categorias: [],
        estado: '',
        numero: 0
      }
      
    }
  },
  methods: {
    ...mapActions(['setTareas', 'cargarLocalStorage']),
    procesarformulario(){
      console.log(this.tarea)
      if(this.tarea.nombre.trim() === ""){
        console.log('Campo vacío')
        return
      }
      console.log('no está vacío')

      // generar id
      this.tarea.id = shortid.generate()
      console.log(this.tarea.id)

      // Se envían datos
      this.setTareas(this.tarea)

      //limpiar datos
      this.tarea = {
        id: '',
        nombre:'',
        categorias: [],
        estado: '',
        numero: 0
      }
    }
  },
  created(){
    this.cargarLocalStorage()
  }

}


</script>
