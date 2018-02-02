<template>
    <div id="infobox">
      <div id="notSupported" v-if="!supported">Browser not supported</div>
      <div v-for="metric in status" v-if="metric.value != null">
        <div>
        <label>{{metric.name}}</label><div> {{metric.value}} {{metric.unit}}</div>
        </div>
      </div>
    </div>
</template>

<script>
  const log = console;
  export default {
    name: 'VueNetworkStatus',
    data() {
      return {
        supported: true,
        status: {
          type: {
            name: 'Type',
            value: undefined,
          },
          effectiveType: {
            name: 'Effective Type',
            value: undefined,
          },
          rtt: {
            name: 'Round Trip Time',
            unit: 'ms',
            value: undefined,
          },
          downlink: {
            name: 'Downlink',
            unit: 'Mb/s',
            value: undefined,
          },
          downlinkMax: {
            name: 'Max Downlink',
            unit: 'Mb/s',
            value: undefined,
          },
        },
      };
    },
    mounted() {
      if (!navigator.connection) {
        log.error('Network API not supported');
        this.supported = false;
      } else {
        log.info('Network API supported');
        navigator.connection.addEventListener('change', this.networkInfoHandler);
        this.networkInfoHandler();
      }
    },
    methods: {
      networkInfoHandler() {
        const c = navigator.connection;

        log.group('Network info event', c);

        // Network type that browser uses
        log.debug('type', c.type);

        // Effective bandwidth estimate
        log.debug('downlink', c.downlink);

        // Effective round-trip time estimate
        log.debug('rtt', c.rtt);

        // Upper bound on the downlink speed of the first network hop
        log.debug('downlinkMax', c.downlinkMax);

        // Effective connection type determined using a combination of recently
        // observed rtt and downlink values: ' +
        log.debug('effectiveType', c.effectiveType);

        log.groupEnd();

        this.status.type.value = c.type;
        this.status.downlink.value = c.downlink;
        this.status.rtt.value = c.rtt;
        this.status.downlinkMax.value = c.downlinkMax;
        this.status.effectiveType.value = c.effectiveType;
      },
    },
  };
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  #infobox {
    display: flex;
    align-content: center;
    align-items: center;
    justify-content: center;
    flex-wrap: wrap;
  }

  #infobox > * {
    margin: 15px;
  }

  #notSupported {
    font-weight: bold;
    color: red;
  }

  label {
    font-weight: bold;
  }
</style>
