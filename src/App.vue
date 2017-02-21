<template>
  <div id="app">
    <h2>Map Editor</h2>

    <layout>
      <map-field slot="content" :rowsCount="rowsCount" :colsCount="colsCount" :map="map"></map-field>
      <controls slot="sidebar" :rowsCount="rowsCount" :colsCount="colsCount">
        <button slot="dump" class="btn-dump" @click="dumpObject()">Dump</button>
        <button slot="dump" class="btn-dump" @click="dumpString()">Dump Stringify</button>
        <div slot="load-map">
          <textarea v-model="textareaMapData" placeholder="Load map data here" class="load-map"></textarea>
          <button class="btn-dump" @click="loadMapData()">Load</button>
        </div>

      </controls>
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
      textareaMapData: [],
      rowsCount: 0,
      colsCount: 0,
      map: {}
    }
  },
  methods: {
    dump () {
      let key = '',
          item = {},
          result = [];

      for (let row = 0; row <= this.rowsCount; row++) { result.push([]); }

      for (let row = 1; row <= this.rowsCount; row++) {
        if (!result[row]) { result.push([]); }

        for (let col = 1; col <= this.colsCount; col++) {
          key = row + '.' + col;

          if (this.map[key]) {
            item = this.map[key];
          } else {
            item = cfg.getTileData();
          }

          if (item.respawn && !item.respawn.isset) {
            delete item.respawn;
          }

          if (!result[row][col]) {
            result[row].push(item);
          } else {
            result[row][col] = item;
          }

        }
      }

      return result;
    },
    dumpObject () {
      console.log(this.dump());
    },
    dumpString () {
      console.log(JSON.stringify(this.dump()));
    },
    loadMapData () {
      let textareaMapData = JSON.parse(this.textareaMapData),
          rowLn = textareaMapData.length,
          colLn = textareaMapData[0].length,
          map = this.map;
//debugger;
      for (let row = 0; row < rowLn; row++) {
        for (let col = 0; col < colLn; col++) {
          map[(row+1) + '.' + (col+1)] = textareaMapData[row][col];
        }
      }

      this.map = { ...map };

      this.rowsCount = rowLn;
      this.colsCount = colLn;

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

.btn-dump {
  margin: 15px 0 0 0;
  padding: 10px;
}

.load-map {
  width: 220px;
  height: 110px;
}

</style>
