<template>
  <div id="app">
    <h2>Map Editor</h2>

    <layout>
      <map-field slot="content" :rowsCount="rowsCount" :colsCount="colsCount" :map="map"></map-field>
      <controls slot="sidebar" :rowsCount="rowsCount" :colsCount="colsCount"></controls>
    </layout>
  </div>
</template>

<script>
import MapField from './components/MapField/MapField.vue';
import Controls from './components/Controls/Controls.vue';
import Layout from './components/Layout/Layout.vue';
import { EventBus } from './EventBus';
import cfg from './config';

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
      rowsCount: 0,
      colsCount: 0,
      map: {}
    }
  },
  created () {
    // --
    EventBus.$on('changeRowsCount', (newRowsCount) => {
      this.rowsCount = newRowsCount;
    });
    // --
    EventBus.$on('changeColsCount', (newColsCount) => {
      this.colsCount = newColsCount;
    });
    // --
    EventBus.$on('toggleRespawn', (data) => {
      var key = data.row + '.' + data.col,
          map = this.map;

      if (!map[key]) {
        map[key] = cfg.getTileData();
      }

      map[key].respawn.isset = !map[key].respawn.isset;

      this.map = { ...map };
    });
    // --
    EventBus.$on('toggleStatic', (data) => {
      var key = data.row + '.' + data.col,
          map = this.map;

      if (!map[key]) {
        map[key] = cfg.getTileData();
      }

      map[key].static = !map[key].static;

      this.map = { ...map };
    });
    // --
    EventBus.$on('changeSurface', (data) => {
      var key = data.row + '.' + data.col,
          map = this.map;

      if (!map[key]) {
        map[key] = cfg.getTileData();
      }

      map[key].surface = data.surface;

      this.map = { ...map };
    });
    // --
    EventBus.$on('changeTeamId', (data) => {
      var key = data.row + '.' + data.col,
          map = this.map;

      if (!map[key]) {
        map[key] = cfg.getTileData();
      }

      map[key].respawn.teamId = +data.teamId;

      this.map = { ...map };
    });


    //
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
