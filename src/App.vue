<template>
  <div id="app">
    <Branch :content="treeContent" />
  </div>
</template>

<script>
import jsonTree from '../public/static/node_modules.json'
import Branch from './components/Branch.vue'

export default {
  name: 'App',
  components: {
    Branch
  },
  data () {
    return {
      treeContent: jsonTree
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  margin-left: 60px;
}
</style>
