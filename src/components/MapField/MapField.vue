<template>
    <div class="map-field">
        <div v-for="row in rowsCount" class="row">
            <div v-for="col in colsCount" class="cell">
                <span class="index">
                    {{row}} / {{col}}
                </span>
                <tile-editor :tileData="getTileData(row, col)" :map="map" :row="row" :col="col"></tile-editor>
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
                type: Object,
                required: true
            }
        },
        components: {
            TileEditor
        },
        methods: {
            getTileData (row, col) {
                let key = row + '.' + col,
                    result = this.map[key] ? this.map[key] : cfg.getTileData();

                return result;
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
