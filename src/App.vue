<template>
  <div id="app">
    <h2>Map Editor</h2>

    <layout>
      <map-field slot="content" :rowsCount="rowsCount" :colsCount="colsCount"></map-field>
      <controls slot="sidebar" :rowsCount="rowsCount" :colsCount="colsCount"></controls>
    </layout>
  </div>
</template>

<script>
import MapField from './components/MapField/MapField.vue';
import Controls from './components/Controls/Controls.vue';
import Layout from './components/Layout/Layout.vue';
import { EventBus } from './EventBus';

export default {
  name: 'app',
  components: {
    MapField,
    Controls,
    Layout
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      rowsCount: 3,
      colsCount: 3,
    }
  },
  created () {
    EventBus.$on('changeRowsCount', (rows) => {
      this.rowsCount = rows;
    });
    EventBus.$on('changeColsCount', (cols) => {
      this.colsCount = cols;
    });
  }
}
</script>

<style lang="scss">

html, body {
  margin: 0;
  height: 100%;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}

h1, h2 {
  font-weight: normal;
}

a {
  color: #42b983;
}
</style>
