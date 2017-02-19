<template>
    <div>
        <input type="text" name="surface" placeholder="surface" size="10"  v-model="surface" />
        <input type="checkbox" :checked="static" :id="generateStaticId" @click="toggleStatic" /><label :for="generateStaticId">Static</label>
        <br>
        <input type="checkbox" :checked="isset" :id="generateRespawnId" @click="toggleRespawn" /><label :for="generateRespawnId">Respawn</label>
        <input v-if="isset" type="text" name="teamId" placeholder="teamId" size="5" v-model="teamId" />
    </div>
</template>

<script>
    import { EventBus } from '../../../EventBus';
    import cfg from '../../../config';

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
            },
            map: {
                type: Object,
                required: true
            }
        },
        name: 'tile-editor',
        computed: {
            generateRespawnId () {
                return "label-respawn-" + this.row + "-" + this.col;
            },

            generateStaticId () {
                return "label-static-" + this.row + "-" + this.col;
            },

            surface: {
                get () {
                    return this.tileData.surface;
                },

                set (newValue) {
                    EventBus.$emit('changeSurface', {
                        row: this.row,
                        col: this.col,
                        surface: newValue
                    });
                }
            },

            teamId: {
                get () {
                    return this.tileData.respawn.teamId;
                },

                set (newValue) {
                    EventBus.$emit('changeTeamId', {
                        row: this.row,
                        col: this.col,
                        teamId: newValue
                    });
                }
            },

            isset () {
                return this.tileData.respawn.isset;
            },

            item () {
                return this.tileData;
            },

            static () {
                return this.tileData.static;
            }
        },
        methods: {
            toggleRespawn () {
                EventBus.$emit('toggleRespawn', {
                    row: this.row,
                    col: this.col
                });
            },

            toggleStatic () {
                EventBus.$emit('toggleStatic', {
                    row: this.row,
                    col: this.col
                });
            }
        }
    };
</script>

<style scoped>
label {
    font-size: 12px;
}
</style>
