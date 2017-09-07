<template>
  <div>
  <h2>Sistema Gestor de Eventos</h2>
  <ul class="nav nav-tabs">
      <li v-for="tab in tabs" class="nav-item">
        <a class="nav-link" :class="{'active' : tab.activated}" data-toggle="tab" :href="tab.href" @click="selectTab(tab)">{{ tab.name }}</a>
      </li>
    </ul>

    <div class="tab-content">
      <tab name="Tipos de Eventos" :selected="true">
        <TipoEventoMaster></TipoEventoMaster>
      </tab>

      <tab name="Eventos" :selected="false">
          <evento-master></evento-master>

      </tab>
    </div>
  </div>
</template>

<script>
  import Tab from './Tab.vue';

  import TipoEventoMaster from '../EventoComponent/TipoEventoMaster.vue';
  import EventoMaster from '../EventoComponent/EventoMaster.vue';


  export default {
    name: 'tab-master',
    components: {
      Tab,
      TipoEventoMaster,
      EventoMaster
    },

    data() {
      return { tabs: [] };
    },

    created() {
      this.tabs = this.$children;
    },

    methods: {
      selectTab(selected_tab) {
        this.tabs.forEach((tab) => {
          tab.activated = (tab.href == selected_tab.href);
        });
        Vue.$emit('close-form');
      }
    }
  };
</script>
<style>
h2{
position:relative;
right:-2px;
padding:8px 63px 6px 17px;
width:100%;
margin:0;
font-size:32px;
background:#4F4F4F; /* Background color */
color:#f2f2f2; /* Color of the widget's title */
text-align:center;
text-indent:18px;
}
h2:before{
position:absolute;
content:"";
top:36px;
right:0px;
width: 0px;
height: 0px;
border-bottom:12px outset transparent;
border-left:12px solid #000000;
}
h2:after{
position:absolute;
content:"";
top:-6px;
left:-5px;
width: 0px;
height: 0px;
border-bottom:24px outset transparent;
border-top:24px outset transparent;
border-left:24px solid #ffffff; /* Arrow background color on the left */
}

</style>
