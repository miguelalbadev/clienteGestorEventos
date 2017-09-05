<template>
	<div class="master row">
	  	<div class="list col-sm-12 col-md-6">
            <button class="btn btn-primary btn-crear" @click="crearTipoEvento">Crear nuevo tipo de evento</button>
            <div class="list-group">
            <a v-for="tipoevento in tipoeventosList" class="list-group-item">
                Descripción: {{tipoevento.Descripcion}} --- Criticidad: {{tipoevento.Criticidad}}
                <button class="btn btn-danger " @click="handleBorrarClick(tipoevento)">Borrar</button>
                <button class="btn btn-default " @click="handleEditarClick(tipoevento)">Editar</button>
                
            </a>
            </div>
			
		</div>
        <TipoEvento @addTipoEvento="cargaListadoTipoEventos" @modifyEvento="onModifyEvento" :api_host="host"></TipoEvento>
	</div>


</template>

<script>
import axios from 'axios';
import TipoEvento from './TipoEvento.vue';

export default {
    name: 'TipoEventoMaster',
    components: {
        TipoEvento
    },
	data:function(){
		return {
			tipoeventosList:[],
            host: 'http://localhost:52730/api/TipoEvento',

		}
	},
    mounted() {
        this.cargaListadoTipoEventos();
    },
    methods: {
        selectTipoEvento: function(tipoEvento) {
            debugger;
        //this.seen=true;
        //this.$emit('selectEntrada', entrada);
        },
        cargaListadoTipoEventos(){
            debugger;
            
            let _this = this;
            _this.tipoeventosList.length = 0;
            axios.get(this.host).then((response) => {
              _this.tipoeventosList = response.data;
            }).catch((error) => {
              //Vue.$emit('show-modal', error.message, error.stack)
            });
        },
        crearTipoEvento(){
            Vue.$emit('show-form', null);
        },
        handleEditarClick(tipoevento){
            Vue.$emit('edit-tipoevento',tipoevento);
        },
        handleBorrarClick(tipoevento){

             axios.delete(this.host + '/' + tipoevento.Id)
                .then((res) => {
                  alert('El Tipo de Evento ha sido borrado con éxito');
                  this.cargaListadoTipoEventos();
                  Vue.$emit('close-form');
             })

        },
        onAddTipoEvento(tipoEvento){

        },
        onModifyEvento(tipoevento){

        }

    }

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
