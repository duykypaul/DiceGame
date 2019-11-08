<template>
    <div>
        <comp-dice v-for="(dice, index) in dices" :key="index" v-bind:dice="dice"/>
    </div>
    
</template>

<script>
import CompDice from './CompDice.vue'
export default {
    name: 'comp-dices',
    props: {
        dices: Array
    },
    data() {
        return {
            
        }
    },
    components: {
        CompDice
    }
}
</script>

<style>

</style>