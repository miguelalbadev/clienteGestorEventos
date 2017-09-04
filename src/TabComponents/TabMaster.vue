<template>
  <div>
    <ul class="nav nav-tabs">
      <li v-for="tab in tabs" class="nav-item">
        <a class="nav-link" :class="{'active' : tab.activated}" data-toggle="tab" :href="tab.href" @click="selectTab(tab)">{{ tab.name }}</a>
      </li>
    </ul>

    <div class="tab-content">
      <tab name="Tipos de Eventos" :selected="true">
        <TipoEvento></TipoEvento>
      </tab>

      <tab name="Eventos" :selected="false">
          <evento-master></evento-master>

      </tab>
    </div>
  </div>
</template>

<script>
  import Tab from './Tab.vue';
  import TipoEvento from '../SingleComponents/TipoEvento.vue';
  import EventoMaster from '../EventoComponent/EventoMaster.vue';

  export default {
    name: 'tab-master',
    components: {
      Tab,
      TipoEvento,
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
      }
    }
  };
</script>
