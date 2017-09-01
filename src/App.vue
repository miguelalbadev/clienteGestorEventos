<template>
  <div id="app">
      <modal></modal>
      <tab-master></tab-master>
  </div>
</template>

<script>
import Modal from './SingleComponents/Modal.vue';
import TabMaster from './TabComponents/TabMaster.vue';

export default {
  name: 'app',
  components: {
    Modal, TabMaster
  },
}
</script>

<style>
</style>
