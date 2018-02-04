<template>
    <div v-if='isVisible()' v-bind:class="{tooltip: true, themedark: theme === 'dark'}">
      <span v-if="tooltip" class="tooltiptext">{{tooltip}}</span>
      <img id="icon" :src="icon">
    </div>
</template>

<script>
  import cloudOn from './icons/ic_cloud_queue_black_24px.svg';
  import cloudOff from './icons/ic_cloud_off_black_24px.svg';

  export default {
    name: 'OnlineStatus',
    props: {
      theme: {
        default: 'bright',
        validator(value) {
          return value === 'bright' || value === 'dark';
        },
      },
      onlineIcon: {
        default: cloudOn,
      },
      offlineIcon: {
        default: cloudOff,
      },
      tooltipOnline: {
        default: 'Online',
      },
      tooltipOffline: {
        default: 'Offline',
      },
    },
    computed: {
      icon() {
        return this.status ? this.onlineIcon : this.offlineIcon;
      },
      tooltip() {
        return this.status ? this.tooltipOnline : this.tooltipOffline;
      },
    },
    data() {
      return {
        status: navigator.onLine,
      };
    },
    mounted() {
      window.addEventListener('online', () => this.statusHandler(true));
      window.addEventListener('offline', () => this.statusHandler(false));
    },
    methods: {
      isVisible() {
        if (this.status) {
          return this.onlineIcon !== '';
        }

        return this.offlineIcon !== '';
      },
      statusHandler(status) {
        this.status = status;
        this.$emit('status-change', status);
      },
    },
  };
</script>
<style scoped>

  #icon {
    width: 100%;
  }

  /* Tooltip */

  .tooltip {
    position: relative;
    display: inline-block;
  }

  .tooltip .tooltiptext {
    visibility: hidden;
    width: 120px;
    background-color: #555;
    color: #fff;
    text-align: center;
    border-radius: 6px;
    padding: 5px 0;
    position: absolute;
    z-index: 1;
    bottom: 125%;
    left: 50%;
    margin-left: -60px;
    opacity: 0;
    transition: opacity 0.3s;
  }

  .tooltip .tooltiptext::after {
    content: "";
    position: absolute;
    top: 100%;
    left: 50%;
    margin-left: -5px;
    border: 5px solid transparent;
    border-top-color: #555;
  }

  .tooltip:hover .tooltiptext {
    visibility: visible;
    opacity: 1;
  }

  .themedark {
    filter: invert(100%);
  }
</style>
