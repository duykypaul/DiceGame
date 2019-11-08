<template >
    <div>
        <comp-player 
            v-for="player in players" 
            :key="player.id"
            v-bind:player="player"
            v-bind:active="active"

        />
    </div>
    
</template>

<script>
import CompPlayer from './Complayer.vue'
export default {
    name: 'comp-players',
    props: {
        players: Array,
        active: Number
    },
    data() {
        return {
            
        }
    },
    components: {
        CompPlayer
    }
}
</script>

<style>

</style>