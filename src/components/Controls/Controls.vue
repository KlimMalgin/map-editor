<template>
    <div>
        <span>Rows ({{rowsCount}})</span>
        <br>
        <button class="btn" @click="addRow">+</button>
        <button class="btn" @click="removeRow">-</button>
        <hr>
        <span>Columns ({{colsCount}})</span>
        <br>
        <button class="btn" @click="addCol">+</button>
        <button class="btn" @click="removeCol">-</button>
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
.btn {
    cursor: pointer;
    padding: 10px 14px;
    font-size: 20px;
}
</style>
