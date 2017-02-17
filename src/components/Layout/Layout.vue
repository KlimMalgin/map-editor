<template>
    <div class="layout">
        <div class="content">
            <slot name="content"></slot>
        </div>
        <div class="sidebar">
            <slot name="sidebar"></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'layout',
        props: {
            /*rowsCount: {
                type: Number,
                required: true
            },
            colsCount: {
                type: Number,
                required: true
            }*/
        },
        //components: {},
        data () {
            return {};
        }
    };
</script>

<style scoped>

    .layout {
        display: table;
        height: 100%;
    }
    .content {
        display: table-cell;
        width: 100%;
    }
    .sidebar {
        display: table-cell;
        min-width: 250px;
        width: 250px;
    }
</style>
