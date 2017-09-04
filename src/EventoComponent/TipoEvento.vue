
<template>
<div class="detail col-sm-12 col-md-6" v-if="tipoevento">
  <form>
    <h3 v-if="tipoevento.Id" class="text-center">Modificando Tipo de Evento</h3>
    <h3 v-else class="text-center">Creando Tipo de Evento</h3>
    
    <div class="form-group">
      <label for="nombre-tipo-evento">Nombre: </label>
      <input type="text" class="form-control" id="nombre-tipo-evento" v-model="tipoevento.Descripcion" />
    </div>
    <div class="form-group">
      <label for="categoria-tipo-evento">Categoría: </label>
      <input type="text" class="form-control" id="categoria-tipo-evento" v-model="tipoevento.Categoria" />
    </div>
    <div class="form-group">
      <label for="criticidad-tipo-evento">Criticidad: </label>
      <input type="text" class="form-control" id="criticidad-tipo-evento" v-model="tipoevento.Criticidad" />
    </div>
    <div class="form-group">
      <label for="descripcion-tipo-evento">Descripción: </label>
      <input type="text" class="form-control" id="descripcion-tipo-evento" v-model="tipoevento.Descripción" />
    </div>
    

    <div class="group-btn">
      <button v-if="tipoevento.Id" class="btn btn-success" @click="handleModificarEvento">Modificar</button>
      <button v-else class="btn btn-success" @click="handleCrearEvento">Crear</button>
      <button class="btn btn-secondary" @click="handleCancelar">Cancelar</button>
    </div>
  </form>
</div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'tipoevento',
  props: ['api_host'],

  data() {
    return {
      tipoevento: null,
      host: this.api_host
    };
  },

  created() {
    let _this = this;
    Vue.$on('show-form', (tipoevento) => {
      _this.tipoevento = tipoevento ? tipoevento : {
        Nombre: '',
        Categoria: '',
        Criticidad: '',
        Descripción: ''
      };
    });

    /*Vue.$on('close-form', () => {
      _this.evento = null
    });*/
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
