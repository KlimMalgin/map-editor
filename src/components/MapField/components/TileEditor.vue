<template>
    <div>
        <input type="text" name="surface" placeholder="surface" size="10" :value="tileData.surface" />
        <input type="checkbox" :checked="tileData.respawn.isset" :id="generateId" @click="toggleRespawn" />
        <label :for="generateId">Respawn</label>
        <input v-if="tileData.respawn.isset" type="text" name="teamId" placeholder="teamId" size="5" />
    </div>
</template>

<script>
    import { EventBus } from '../../../EventBus';
    export default {
        props: {
            tileData: {
                type: Object,
                required: true
            },
            row: {
                type: Number,
                required: true
            },
            col: {
                type: Number,
                required: true
            }
        },
        name: 'tile-editor',
        computed: {
            generateId () {
                return "label-" + this.row + "-" + this.col;
            }
        },
        methods: {
            toggleRespawn () {
                //this.tileData.respawn.isset = !this.tileData.respawn.isset;
                EventBus.$emit('toggleRespawn', {
                    row: this.row,
                    col: this.col
                });
            }
        },
        data () {
            return {

            };
        }
    };
</script>

<style scoped>
label {
    font-size: 12px;
}
</style>
