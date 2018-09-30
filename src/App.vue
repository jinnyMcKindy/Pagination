<template>
  <div id="app">
    <Pagination
      :rightIcon="rightIcon"
      :leftIcon="leftIcon"
      :results="results"
      :maxAmountOfPages="maxAmountOfPages"
      :perPage="perPage"
    />
  </div>
</template>
<script>
import Pagination from './components/Pagination'

export default {
  name: 'App',
  components: {
    Pagination
  },
 data () { return {
       leftIcon : "<",
       rightIcon: ">",
       results : [
            {title : "Title1", description : "Description", url : "www.google.com"},
            {title : "Title2", description : "Description", url : "www.google.com"},
            {title : "Title3", description : "Description", url : "www.google.com"},
            {title : "Title4", description : "Description", url : "www.google.com"},
            {title : "Title5", description : "Description", url : "www.google.com"},
            {title : "Title6", description : "Description", url : "www.google.com"},
            {title : "Title7", description : "Description", url : "www.google.com"},
            {title : "Title8", description : "Description", url : "www.google.com"},
            {title : "Title9", description : "Description", url : "www.google.com"},
            {title : "Title10", description : "Description", url : "www.google.com"},
            {title : "title11", description : "Description", url : "www.google.com"},
            {title : "Title12", description : "Description", url : "www.google.com"},
            {title : "Title13", description : "Description", url : "www.google.com"},
            {title : "Title14", description : "Description", url : "www.google.com"},
            {title : "Title15", description : "Description", url : "www.google.com"},
            {title : "Title16", description : "Description", url : "www.google.com"},
            {title : "Title17", description : "Description", url : "www.google.com"},
            {title : "Title18", description : "Description", url : "www.google.com"},
            {title : "Title19", description : "Description", url : "www.google.com"},
            {title : "Title20", description : "Description", url : "www.google.com"},
            {title : "Title21", description : "Description", url : "www.google.com"},
            {title : "Title22", description : "Description", url : "www.google.com"},
            {title : "Title23", description : "Description", url : "www.google.com"},
            {title : "Title24", description : "Description", url : "www.google.com"},
            {title : "Title25", description : "Description", url : "www.google.com"},
            {title : "Title26", description : "Description", url : "www.google.com"},
            {title : "Title27", description : "Description", url : "www.google.com"},
            {title : "Title28", description : "Description", url : "www.google.com"},
            {title : "Title29", description : "Description", url : "www.google.com"},
            {title : "Title30", description : "Description", url : "www.google.com"},
            {title : "Title31", description : "Description", url : "www.google.com"},
            {title : "Title32", description : "Description", url : "www.google.com"},
        ],
        maxAmountOfPages : 5,
        perPage : 4,
      }
  }
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
