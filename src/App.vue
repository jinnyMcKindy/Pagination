
<template>
  <div id="app">
    <Pagination v-bind:msg="msg"/>
  </div>
</template>

<script>
import Pagination from './components/Pagination'

export default {
  name: 'App',
  components: {
    Pagination
  },
 data () { return {  } }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
