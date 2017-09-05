
<template>
<div class="detail col-sm-12 col-md-6" v-if="evento">
  <form>
    <h3 v-if="evento.Id" class="text-center">Modificando Evento</h3>
    <h3 v-else class="text-center">Creando Evento</h3>

    <div class="form-group">
      <label for="fecha-evento">Fecha: </label>
      <input type="date" class="form-control" id="fecha-evento" v-model="evento.Fecha" />
    </div>
    <div class="form-group">
      <label for="descripcion-evento">Descripcion: </label>
      <input type="text" class="form-control" id="descripcion-evento" v-model="evento.Descripcion" />
    </div>
    <div class="form-group">
      <label for="tipo-evento">Tipo: </label>
      <input type="text" class="form-control" id="tipo-evento" v-model="evento.Tipo" />
    </div>
    <div class="form-group">
      <label for="origen-evento">Origen: </label>
      <input type="text" class="form-control" id="origen-evento" v-model="evento.Origen" />
    </div>
    <div class="form-group">
      <label for="destino-evento">Destino: </label>
      <input type="text" class="form-control" id="destino-evento" v-model="evento.Destino" />
    </div>
    <div class="form-group">
      <label for="prioridad-evento">Prioridad: </label>
      <input type="text" class="form-control" id="prioridad-evento" v-model="evento.Prioridad" />
    </div>

    <div class="group-btn">
      <button v-if="evento.Id" class="btn btn-success" @click="handleModificarEvento">Modificar</button>
      <button v-else class="btn btn-success" @click="handleCrearEvento">Crear</button>
      <button class="btn btn-secondary" @click="handleCancelar">Cancelar</button>
    </div>
  </form>
</div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'evento',
  props: ['api_host'],

  data() {
    return {
      evento: null,
      host: this.api_host
    };
  },

  created() {
    let _this = this;
    Vue.$on('show-form', (evento) => {
      _this.evento = evento ? evento : {
        Fecha: '',
        Descripcion: '',
        Tipo: '',
        Origen: '',
        Destino: '',
        Prioridad: ''
      };
    });

    Vue.$on('close-form', () => {
      _this.evento = null
    });

    Vue.$on('edit-evento',(evento)=>{
      _this.evento = evento
    });
  },

  methods: {
    /* SERVER REQUESTS */
    updateEvento() {

    },

    createEvento() {

    },

    /* HANDLE SELF EVENTS */
    handleModificarEvento() {

    },

    handleCrearEvento() {

    },

    handleCancelar() {

    }
  }
}
</script>

<style>
</style>
