<template>
    <board :size="boardSize"/>

</template>

<script>
import Board from "@/components/Board.vue";

export default {
    name: 'App',
    data() {
        return {
            boardSize: 15,
        }

    },
    components: {
        Board,
    },
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}

</style>
