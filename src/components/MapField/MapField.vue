<template>
    <div class="map-field">
        <div v-for="row in rowsCount" class="row">
            <div v-for="col in colsCount" class="cell">
                {{row}} / {{col}}
                <tile-editor></tile-editor>
            </div>
        </div>
    </div>
</template>

<script>
    import TileEditor from './components/TileEditor.vue';
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
            }
        },
        components: {
            TileEditor
        },
        data () {
            return {};
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
        display: table-cell;
        border: 1px solid #ccc;
        width: 100px;
        height: 100px;
    }
</style>
