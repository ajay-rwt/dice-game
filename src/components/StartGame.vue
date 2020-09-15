<template>
  <div>
    <h3>Start a new game :</h3>
    <button @click="gameWasStarted">Start Game</button>
  </div>
</template>

<script>
export default {
  prop: {
    gameIsRunning: Boolean,
  },
  methods: {
    gameWasStarted() {
      this.gameIsRunning = !this.gameIsRunning;
      this.$emit("gameWasStarted", this.gameIsRunning);
    },
  },
};
</script>

<style scoped>
</style>