<template>
  <div class="master row">
    <div class="list col-sm-12 col-md-6">
      <button class="btn btn-primary btn-crear" @click="handleCrearNuevoEventoClick">Crear nuevo evento</button>
      <div class="list-group">
        <a v-for="evento in eventos" class="list-group-item">
          Descripción: {{ evento.Tipo }} --- Fecha: {{evento.Fecha}}
          <button class="btn btn-danger" @click="handleBorrarClick(evento)">Borrar</button>
          <button class="btn btn-default" @click="handleEditarClick(evento)">Editar</button>
        </a>
      </div>
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
  .list-group-item button {
    float: right;
    margin-left: 5px;
  }

  .list-group-item {
    padding-top: 12.5px;
    padding-bottom: 25px;
  }

  .master {
    padding: 20px;
  }

  .btn-crear {
    width: 100%;
    margin: 5px 0 5px 0;
  }

</style>
