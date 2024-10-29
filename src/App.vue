<template>
  <div>
    <TicTacToe />
  </div>
</template>

<script>
import TicTacToe from "./components/tic-tac-toe/TicTacToe.component.vue";
export default {
  components: {
    TicTacToe,
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

div {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}
</style>
