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
      map: []
    }
  },
  created () {
    // --
    EventBus.$on('changeRowsCount', (newRowsCount) => {
      /*if (this.rowsCount < newRowsCount) {
        this.map.push(createArray(newRowsCount, cfg.tileData));
      }
      else if (this.rowsCount > newRowsCount) {
        this.map.pop();
      }*/
      this.rowsCount = newRowsCount;
    });
    // --
    EventBus.$on('changeColsCount', (newColsCount) => {

      /*if (this.colsCount < newColsCount) {
        // Добавили столбец
        //this.map.push(createArray(newColsCount, cfg.tileData));
        addColumn(this.map, newColsCount, cfg.tileData);
      }
      else if (this.colsCount > newColsCount) {
        // Удалили столбец
        removeColumn(this.map, cfg.tileData);
      }*/

      this.colsCount = newColsCount;
    });
    // --
    EventBus.$on('toggleRespawn', (data) => {
      console.log('toggleRespawn: ', data, this.map/*[data.row][data.col]*/);
    });
  }
}

/**
 * Создаст массив заданной длины ln и заполнит его объектами defaultModel
 */
/*function createArray (ln, defaultModel) {
  let arr = [];

  for (let i = 0; i < ln; i++) {
    arr.push(defaultModel);
  }
  return arr;
}*/

/*function addColumn (map, colsCount, defaultModel) {
  let ln = map.length,
      colLn = 0;

  for (let i = 0; i < ln; i++) {
    colLn = colsCount - map[i].length;
    for (let j = 0; j < colLn; j++) {
      map[i].push(defaultModel);
    }
  }
}

function removeColumn (map, defaultModel) {
  let ln = map.length;

  for (let i = 0; i < ln; i++) {
    map[i].pop();
  }
}*/

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
