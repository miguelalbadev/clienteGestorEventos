<template>
	<div class="master row">
	  	<div class="list">
		  	<ul class="list-group col-xs-6 container">
            <button class="list-group-item" @click="">Crear nuevo evento</button>
			  <li class="list-group-item" v-for="tipoevento in tipoeventosList">
			  <a href="#" class="list-group-item list-group-item-action">
         
                  Nombre: {{tipoevento.Descripcion}} --- Criticidad: {{tipoevento.Criticidad}}
                  <button class="btn btn-default " @click="handleEditarClick(evento)">Editar</button>
                <button class="btn btn-danger " @click="handleBorrarClick(evento)">Borrar</button>
              </a>
			    
			    
			  </li>
			</ul>
		</div>
		
	</div>

  
</template>

<script>
import axios from 'axios';

export default {
    name: 'TipoEvento',
	data:function(){
		return {
			tipoeventosList:[],
            host: 'http://10.60.23.21:52730/api/TipoEvento',
            
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
            let _this = this;
            axios.get(this.host).then((response) => {
              _this.tipoeventosList = response.data;
            }).catch((error) => {
              Vue.$emit('show-modal', error.message, error.stack)
            });
        }
    }
  
}
</script>

<style>

button{
    float: right
}
</style>
