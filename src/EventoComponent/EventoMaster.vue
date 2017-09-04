<template>
  <div class="master row">
    <div class="list">
      <ul class="list-group col-xs-6 container">
        <button class="list-group-item" @click="handleCrearNuevoEventoClick">Crear nuevo evento</button>
        <li v-for="evento in eventos" class="list-group-item">
          {{ evento.Descripcion }}
          <button class="btn btn-default float-right" @click="handleEditarClick(evento)">Editar</button>
          <button class="btn btn-danger float-right" @click="handleBorrarClick(evento)">Borrar</button>
        </li>
      </ul>
    </div>

    <evento @addEvento="onAddEvento" @modifyEvento="onModifyEvento" :api_host="host"></evento>
  </div>
</template>

<script>
  import Evento from './Evento.vue';
  import axios from 'axios';

  export default {
    name: 'evento-master',

    components: {
        Evento
    },

    data() {
      return {
        eventos: [],
        host: 'http://localhost:52730/api/Evento',
      };
    },

    created() {
      this.getAllEventos();
    },

    methods: {
      /* SERVER REQUESTS */
      getAllEventos() {
        let _this = this;
        axios.get(this.host).then((response) => {
          _this.eventos = response.data;
        }).catch((error) => {
          Vue.$emit('show-modal', error.message, error.stack)
        });
      },

      deleteEvento(evento) {
        let _this = this;
        axios.delete(this.host + '/' + evento.Id).then((response) => {
          let index = _this.eventos.indexOf(evento);
          _this.eventos.splice(index, 1);
        }).catch((error) => {
          Vue.$emit('show-modal', error.message, error.stack);
        });
      },

      /* HANDLE SELF EVENTS */
      handleCrearNuevoEventoClick() {
        Vue.$emit('show-form', null);
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
  .list-group-item::after {
      content: '';
      clear: both;
  }

</style>
