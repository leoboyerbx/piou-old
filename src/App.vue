<template>
  <div id="app">
    <div>
      <input type="number" min="4" v-model="linesNum">
    </div>
    <Grapes :lines="linesNum" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import Grapes from './components/Grapes.vue'

export default Vue.extend({
  name: 'App',
  components: {
    Grapes
  },
  data () {
    return {
      linesNum: 4
    }
  }
})
</script>

<style lang="scss">
#app {

}
</style>
