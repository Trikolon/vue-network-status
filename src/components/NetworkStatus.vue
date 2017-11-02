<template>
  <div>
    <h1>Network status</h1>
    <div id="infobox">
      <div v-for="metric in status">
        <div v-if="metric.value"><label>{{metric.name}}</label> {{metric.value}} {{metric.unit}}</div>
      </div>
    </div>
  </div>
</template>

<script>
  const log = console;
  export default {
    name: 'HelloWorld',
    data() {
      return {
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
            name: 'Round Trip Time (RTT)',
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
      } else {
        log.debug('Network API supported, mounting...');
      }
      navigator.connection.addEventListener('change', this.networkInfoHandler);
      this.networkInfoHandler();
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
  }

  #infobox > * {
    margin: 5px;
  }

  label {
    font-weight: bold;
  }
</style>
