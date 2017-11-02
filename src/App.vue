<template>
  <div id="app">
    <img src="./assets/logo.png">
    <NetworkStatus/>
  </div>
</template>

<script>
import NetworkStatus from './components/NetworkStatus';

export default {
  name: 'app',
  components: {
    NetworkStatus,
  },
};
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
