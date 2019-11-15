<template>
  <div id="app">
    <h1>A TO-DO LIST APPLICATION</h1>
    <Activity/>
  </div>
</template>

<script>
import Activity from './components/Activity.vue'

export default {
  name: 'app',
  components: {
    Activity
  }
}
</script>

<style>
body {
  background-color: #EEEEEE;
  font-family: 'Montserrat', sans-serif;
  display: grid;
  grid-template-rows: auto;
  justify-items: center;
  padding-top: 150px;
}
body, html {
  margin: 0;
  height: 100%;
}
#app {
    width: 50%;
}
h1{
  text-align: center;
}
</style>
