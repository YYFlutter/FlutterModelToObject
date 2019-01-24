<template>
  <div id="app">
    <FlutterModelToObject/>
  </div>
</template>

<script>
import FlutterModelToObject from "./components/FlutterModelToObject.vue";

export default {
  name: "app",
  components: {
    FlutterModelToObject
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
