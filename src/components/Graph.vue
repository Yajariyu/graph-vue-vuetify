<template>
  <div>
      <Selection :data="data" class="selection"/>
  </div>

</template>

<script>
import Selection from './Selection.vue'
export default {
  name: 'Graph',
  components: {
    Selection
  },
  props:  {
    data: {
      type: Object,
      default: null
    },
  },
}
</script>

<style>
  .selection{
    height:100vh
  }
</style>
