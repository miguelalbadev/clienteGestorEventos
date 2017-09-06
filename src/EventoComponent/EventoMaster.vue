<template>
  <div class="master row">
    <div class="list col-sm-12 col-md-6">
      <button class="btn btn-primary btn-crear" @click="handleCrearNuevoEventoClick">Crear nuevo evento</button>
      <div class="list-group">
        <a v-for="evento in eventos" class="list-group-item clearfix">
          <span class="col-sm-8">Descripción: {{ evento.Descripcion }} --- Fecha: {{ evento.Fecha }}</span>
          <div class="master-button-group col-sm-12 col-md-4">
            <button class="btn btn-default col-12" @click="handleEditarClick(evento)">Editar</button>
            <button class="btn btn-danger col-12" @click="handleBorrarClick(evento)">Borrar</button>
          </div>
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

      Vue.$on('refresh-eventos', () => {
        this.getAllEventos();
      })
    },

    methods: {
      /* SERVER REQUESTS */
      getAllEventos() {
        let _this = this;
        _this.eventos.length = 0;

        axios.get(this.host).then((response) => {
          _this.eventos = response.data;
          this.eventos.forEach((evento) => {
            evento.Fecha = moment(evento.Fecha).format('DD/MM/YYYY h:mm a');
          });
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
          Vue.$emit('edit-evento',evento);
      },

      handleBorrarClick(evento) {
          axios.delete(this.host + '/' + evento.Id)
                .then((res) => {
                  Vue.$emit('show-modal', 'Evento eliminado', 'El Evento ha sido eliminado con éxito');
                  this.getAllEventos();
                  Vue.$emit('close-form');
             })
      },

      /* HANDLE CHILDREN EVENTS */
      onAddEvento(evento) {
        this.eventos.push(evento);
      },

      onModifyEvento(eventoModified) {
        this.eventos.forEach((evento) => {
          if (evento.Id == eventoModified.Id){
            evento = eventoModified;
          }
        });
      },
    },
  }
</script>

<style>
  .list-group-item span {
    display: block;
    padding: 10px;
    max-width: 100%;
    word-wrap: break-word;
  }

  .master-button-group {
    padding-left: 30px;
    padding-right: 0px;
  }

  .master-button-group button {
    width: 75px;
    margin-left: 5px;
    margin-bottom: 5px;
  }

  .master {
    padding: 20px;
  }

  .btn-crear {
    width: 100%;
    margin: 5px 0 5px 0;
  }

</style>
