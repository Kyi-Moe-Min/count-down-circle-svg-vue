<template>
  <div id="app">
    <CountDownCircle/>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import CountDownCircle from "./components/CountDownCircle";

export default {
  name: "App",
  components: {
    HelloWorld,
    CountDownCircle
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
