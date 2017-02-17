<template>
    <div>
        <button @click="addRow">addRow</button>
        <button @click="removeRow">removeRow</button>
        <br />
        <span>/</span>
        <br />
        <button @click="addCol">addCol</button>
        <button @click="removeCol">removeCol</button>
    </div>
</template>

<script>
    import { EventBus } from '../../EventBus';
    export default {
        name: 'controls',
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
        //components: {},
        data () {
            return {

            };
        },
        methods: {
            addRow () {
                EventBus.$emit('changeRowsCount', this.rowsCount + 1);
            },
            removeRow () {
                EventBus.$emit('changeRowsCount', this.rowsCount > 0 ? this.rowsCount - 1 : 0);
            },
            addCol () {
                EventBus.$emit('changeColsCount', this.colsCount + 1);
            },
            removeCol () {
                EventBus.$emit('changeColsCount', this.colsCount ? this.colsCount - 1 : 0);
            }
        }
    };
</script>

<style scoped>

</style>
