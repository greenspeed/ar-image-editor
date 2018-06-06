<template>
  <div id="app">
    <ImageEditor msg="Welcome to editor App"/>
  </div>
</template>

<script>
import ImageEditor from './components/ImageEditor.vue'

export default {
  name: 'app',
  components: {
    ImageEditor
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
  padding: 60px 0 60px 0;
  background-color: #f5f5f5;
}
</style>
