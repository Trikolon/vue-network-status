<template>
  <div id="app">
    <h1>Network Status</h1>
    <p>
      These metrics are reported by your browser and therefore might be inaccurate.
      Try
      <a href="https://play.google.com/store/apps/details?id=com.android.chrome" rel="noopener" target="_blank">
        Google Chrome on Android
      </a> for the best results.</p>
    <p>Data is updated automatically.</p>

    <div id="networkStatus">
      <OnlineStatus />
      <NetworkInfo/>
    </div>
  </div>
</template>

<script>
import NetworkInfo from './components/NetworkInfo.vue';
import OnlineStatus from './components/OnlineStatus.vue';

export default {
  name: 'app',
  components: {
    NetworkInfo,
    OnlineStatus,
  },
};
</script>

<style>
  #app {
  @import url('https://fonts.googleapis.com/css?family=Roboto');
    font-family: 'Roboto', sans-serif;
    text-align: center;
    margin: 5em;
  }
  #networkStatus {
    margin: 20px;
  }
</style>
