<template>
  <div id="app">
    <Modal />
  </div>
</template>

<script>

import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    Modal
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  outline: none;
}
#app {
  margin-top: 50px;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  background: #1670d1;
}

@media (max-width: 600px) {
  #app {
    padding: 15px;
}
}
</style>
