<template>
<div class='input-group date' ref="datetimepicker" id="datetimepicker">
  <input type='text' class="form-control" :value="date" @change="update($event)" />
  <span class="input-group-addon">
      <span class="glyphicon glyphicon-calendar"></span>
  </span>
</div>
</template>

<script>
// Import this component
import datePicker from 'vue-bootstrap-datetimepicker';

export default {
  name: 'datetimepicker',
  props: ['value'],

  components: {
      datePicker
  },

  data() {
    return {
      date: this.value,
    };
  },

  mounted() {
    this.date = moment(this.value).format('DD/MM/YYYY h:mm a');
    $(this.$refs.datetimepicker).datetimepicker()
  },

  methods: {
    update(event) {
      this.$emit('input', event.target.value);
    }
  },

};
</script>
