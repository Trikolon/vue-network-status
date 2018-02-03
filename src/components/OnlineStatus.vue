<template>
    <div v-if='isVisible()' class="tooltip">
      <span class="tooltiptext">{{status ? tooltipOnline : tooltipOffline}}</span>
      <i class="material-icons">{{status ? this.onlineIcon : this.offlineIcon}}</i>
    </div>
</template>

<script>
  const log = console;
  export default {
    name: 'OnlineStatus',
    props: {
      onlineIcon: {
        default: 'cloud_queue',
      },
      offlineIcon: {
        default: 'cloud_off',
      },
      tooltipOnline: {
        default: 'Online',
      },
      tooltipOffline: {
        default: 'Offline',
      },
    },
    data() {
      return {
        status: navigator.onLine,
      };
    },
    beforeDestroy() {
      log.debug('OnlineStatus DESTROY', this);
    },
    mounted() {
      log.debug('OnlineStatus MOUNTED', this);

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

  /* Material icons  */
  @font-face {
    font-family: 'Material Icons';
    font-style: normal;
    font-weight: 400;
    src: url(~material-design-icons/iconfont/MaterialIcons-Regular.eot); /* For IE6-8 */
    src: local('Material Icons'),
    local('MaterialIcons-Regular'),
    url(~material-design-icons/iconfont/MaterialIcons-Regular.woff2) format('woff2'),
    url(~material-design-icons/iconfont/MaterialIcons-Regular.woff) format('woff'),
    url(~material-design-icons/iconfont/MaterialIcons-Regular.ttf) format('truetype');
  }
  .material-icons {
    font-family: 'Material Icons';
    font-weight: normal;
    font-style: normal;
    font-size: 24px;  /* Preferred icon size */
    display: inline-block;
    line-height: 1;
    text-transform: none;
    letter-spacing: normal;
    word-wrap: normal;
    white-space: nowrap;
    direction: ltr;

    /* Support for all WebKit browsers. */
    -webkit-font-smoothing: antialiased;
    /* Support for Safari and Chrome. */
    text-rendering: optimizeLegibility;

    /* Support for Firefox. */
    -moz-osx-font-smoothing: grayscale;

    /* Support for IE. */
    font-feature-settings: 'liga';
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
</style>
