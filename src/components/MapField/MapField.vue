<template>
    <div class="map-field">
        <div v-for="row in rowsCount" class="row">
            <div v-for="col in colsCount" class="cell">
                <span class="index">
                    {{rowsCount}} / {{colsCount}}
                </span>
                <tile-editor :tileData="getTileData()" :row="rowsCount" :col="colsCount"></tile-editor>
            </div>
        </div>
    </div>
</template>

<script>
    import TileEditor from './components/TileEditor.vue';
    import cfg from '../../config';

    export default {
        name: 'map-field',
        props: {
            rowsCount: {
                type: Number,
                required: true
            },
            colsCount: {
                type: Number,
                required: true
            },
            map: {
                type: Array,
                required: true
            }
        },
        components: {
            TileEditor
        },
        methods: {
            getTileData (row, col) {
                if (this.map[row] && this.map[row][col]) {
                    return this.map[row][col];
                } else {
                    return cfg.tileData;
                }
            }
        }
    };
</script>

<style scoped>
    .map-field {
        display: table;
    }

    .row {
        display: table-row;
    }

    .cell {
        text-align: left;
        display: table-cell;
        border: 1px solid #ccc;
        width: 70px;
        height: 70px;
    }

    .index {
        vertical-align: top;
        font-size: 10px;
        color: #999;
    }
</style>
