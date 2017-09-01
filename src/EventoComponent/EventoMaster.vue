<template>
  <div class="master">
    <div class="detail">
      <button class="btn btn-primary" @click="this.handleCrearNuevoEventoClick">Crear nuevo evento</button>
      <ul>
        <li v-for="evento in eventos" >
          {{ evento.Nombre }}
          <button class="btn btn-default" @click="this.handleEditarClick(evento)">Editar</button>
          <button class="btn btn-danger"@click="this.handleBorrarClick(evento)">Borrar</button>
        </li>
      </ul>
    </div>

    <evento @addEvento="" @modifyEvento=""></evento>
  </div>
</template>

<script>
  import Evento from './Evento.vue';
  import axios from 'axios';

  export default {
    name: 'evento-master',
    data() {
      return {
        eventos: [],
        host: 'http://localhost:8080/api/Eventos',
      };
    },

    created() {
      this.getAllEventos();
    },

    methods: {
      /* SERVER REQUESTS */
      getAllEventos() {
        axios.get(this.host).then((response) => {

        }).catch((error) => {

        });
      },

      deleteEvento(evento) {
        axios.delete(this.host + '/' + evento.Id).then((response) => {

        }).catch((error) => {

        });
      },

      /* HANDLE SELF EVENTS */
      handleCrearNuevoEventoClick() {

      },

      handleEditarClick(evento) {

      },

      handleBorrarClick(evento) {

      },

      /* HANDLE CHILDREN EVENTS */
      onAddEvento(evento) {

      },

      onModifyEvento(evento) {

      },

    },
  }
</script>

<style>
</style>
