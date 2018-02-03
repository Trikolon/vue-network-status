<template>
    <div v-if='isVisible()'>
      <!-- TODO: tooltip -->
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
      tooltip: {
        default: 'Network Status',
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
</style>
