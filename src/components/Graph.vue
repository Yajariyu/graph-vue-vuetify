<template>
  <div>
      <Selection :data="data"/>
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

</style>
