<template>
  <div id="app">
      <my-upload :multiple="true" ></my-upload>
  </div>
</template>

<script>
import myUpload from './components/upload.vue'

export default {
  name: 'app',
  components: {
    myUpload
  }
}
</script>

<style lang="less">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 60px auto 0;
  width:900px;
}
</style>
