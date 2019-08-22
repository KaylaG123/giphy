<template>
  <div id="app">
      <gif-search></gif-search>
      <result></result>

  </div>
</template>

<script>
import gifSearch from './components/gifSearch.vue'
import result from './components/result.vue'

export default {
  name: 'app',
  components: {
      gifSearch,
      result
  }
}
</script>

<style>


</style>
