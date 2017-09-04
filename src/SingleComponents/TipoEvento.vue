<template>
	<div>
	  	<div class="list-group">
		  	<ol>
			  <li class="list-group-item" v-for="tipoevento in tipoeventosList">
			  <a class="list-group-item list-group-item-action" @href.prevent="" v-on:click="selectTipoEvento(tipoevento)">
			    {{tipoevento.Nombre}} {{tipoevento.Criticidad}}
			   </a>
			  </li>
			</ol>
		</div>
		<!--<detalleEntradas v-on:updateEntradas="cargaListadoEntradas" v-show="seen"></detalleEntradas>-->
	</div>

  
</template>

<script>
//import detalleEntradas from './detalleEntradas'

export default {
    name: 'TipoEvento',
	data:function(){
		return {
			tipoeventosList:[{
                Nombre:"Alarmas incencios",
                Criticidad:"Media"}]
            
		}
	},
    mounted() {
        //this.cargaListadoTipoEventos();
    },
    methods: {
        selectTipoEvento: function(tipoEvento) {
            debugger;
        //this.seen=true;
        //this.$emit('selectEntrada', entrada);
        },
        cargaListadoTipoEventos(){
            let _this = this;     
            _this.tipoeventosList.length = 0;
            $.ajax({

                url: "http://10.60.23.21:52730/api/TipoEvento/",
                type: 'GET',

                // el tipo de información que se espera de respuesta
                dataType: 'json',

                // código a ejecutar si la petición es satisfactoria;
                // la respuesta es pasada como argumento a la función
                success: function(data) {
                  debugger;
                  

                },
                error: function(xhr, status) {
                  // debugger;
                },
                // código a ejecutar sin importar si la petición falló o no
                complete: function(xhr, status) {
                  //alert('Petición realizada');
                }
            });
        }
    }
  
}
</script>

<style>

</style>
