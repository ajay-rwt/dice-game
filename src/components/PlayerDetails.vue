<template>
  <div id="pl-details">
    <p>Player 1 Name : {{ playerOne.name }}</p>
    <input type="text" @change="playerOne.name = $event.target.value" />
    <p>Player 2 Name : {{ playerTwo.name }}</p>
    <input type="text" @change="playerTwo.name = $event.target.value" />
    <p>Win Target : {{ winTarget }}</p>
    <input type="text" @change="winTarget = parseInt($event.target.value)" />
    <br />
    <br />
    <button @click="inTheGame">Go!</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      playerOne: {
        name: "",
      },
      playerTwo: {
        name: "",
      },
      winTarget: 0,
    };
  },
  methods: {
    inTheGame() {
      this.$emit("inTheGame", true);
      this.$emit("gameDetailsProvided", {
        playerOne: this.playerOne,
        playerTwo: this.playerTwo,
        winTarget: this.winTarget,
      });
    },
  },
};
</script>

<style scoped>
#pl-details {
}
</style>