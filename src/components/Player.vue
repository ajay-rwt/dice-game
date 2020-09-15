<template>
  <div class="maindiv" :class="{'active': isActive}">
    <h1>{{ name }}</h1>
    <div id="dice">
      <h1>Current Score : {{ currentScore }}</h1>
    </div>
    <button @click="getCurrentScore">Roll</button>
    <button @click="updateTotalScoreAndDeactivate" v-if="didIRollDice">Hold</button>
    <h1>Total Score : {{ totalScore }}</h1>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      totalScore: 0,
      currentScore: 0,
      didIRollDice: false,
    };
  },
  props: {
    isFirstPlayer: Boolean,
    name: { type: String, default: "PLAYER 1" },
    winTarget: { type: Number, required: true },
    isActive: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    getCurrentScore() {
      if (this.isActive) {
        this.currentScore = Math.floor(Math.random() * 6) + 1;
        this.didIRollDice = true;
        if (this.currentScore === 1) {
          this.isActive = false;
          this.currentScore = 0;
          this.didIRollDice = false;
          alert("Oops! Onsie means other's turn");
          this.$emit("turnGotOver", this.totalScore, this.name);
        }
      }
    },
    updateTotalScoreAndDeactivate() {
      if (this.isActive) {
        this.totalScore += this.currentScore;
        this.isActive = false;
        this.currentScore = 0;
        this.didIRollDice = false;
        this.$emit("turnGotOver", this.totalScore, this.name);
      }
    },
  },
};
</script>

<style scoped>
.maindiv {
  width: 50%;
  box-sizing: border-box;
  padding: 10px;
  background-color: gainsboro;
  color: grey;
}

.active {
  background-color: greenyellow;
  color: black;
}
</style>