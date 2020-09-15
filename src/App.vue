<template>
  <div id="app">
    <StartGame id="start-game" v-if="!gameIsRunning" @gameWasStarted="gameHasStarted($event)"></StartGame>
    <PlayerDetails
      id="player-details"
      v-if="gameIsRunning && !inTheGame"
      @inTheGame="whenInTheGame"
      @gameDetailsProvided="setupPlayerDetails"
    ></PlayerDetails>
    <div id="players" v-if="gameIsRunning && inTheGame">
      <h2>WIN TARGET : {{ gameDetails.winTarget }}</h2>
      <div id="sub-player">
        <Player
          :isFirstPlayer="true"
          :isActive="isPlayerOneActive"
          :name="gameDetails.playerOne.name"
          :winTarget="gameDetails.winTarget"
          @turnGotOver="processGame"
        ></Player>
        <Player
          :isActive="isPlayerTwoActive"
          :name="gameDetails.playerTwo.name"
          :winTarget="gameDetails.winTarget"
          @turnGotOver="processGame"
        ></Player>
      </div>
      <br />
      <br />
      <button @click="quitGame">Quit</button>
    </div>
  </div>
</template>

<script>
import StartGame from "./components/StartGame.vue";
import PlayerDetails from "./components/PlayerDetails.vue";
import Player from "./components/Player.vue";

export default {
  components: {
    StartGame,
    PlayerDetails,
    Player,
  },
  data: function () {
    return {
      gameIsRunning: false,
      inTheGame: false,
      gameDetails: {},
      isPlayerOneActive: true,
      isPlayerTwoActive: false,
    };
  },
  methods: {
    gameHasStarted(gameIsRunning) {
      this.gameIsRunning = gameIsRunning;
    },
    whenInTheGame(inTheGame) {
      this.inTheGame = inTheGame;
      if (Math.floor(Math.random() * 2) + 1 === 1) {
        this.isPlayerOneActive = true;
        this.isPlayerTwoActive = false;
      } else {
        this.isPlayerOneActive = false;
        this.isPlayerTwoActive = true;
      }
    },
    quitGame() {
      this.gameIsRunning = !this.gameIsRunning;
      this.inTheGame = !this.inTheGame;
      this.gameDetails = null;
      this.isPlayerOneActive = false;
      this.isPlayerTwoActive = false;
    },
    setupPlayerDetails(gameDetails) {
      this.gameDetails = gameDetails;
    },
    processGame(playersTotalScore, playerName) {
      console.log("__________", playersTotalScore, playerName);
      if (playersTotalScore >= this.gameDetails.winTarget) {
        alert(playerName + " wins!!!");
        this.quitGame();
      } else {
        if (playerName === this.gameDetails.playerOne.name) {
          console.log("heeere - ");
          this.isPlayerOneActive = false;
          this.isPlayerTwoActive = true;
        } else {
          this.isPlayerTwoActive = false;
          this.isPlayerOneActive = true;
        }
      }
    },
  },
};
</script>

<style scoped>
#app {
  height: 550px;
  width: 70%;
  margin: 100px auto 0 auto;
  font-family: "Dosis", sans-serif;
}

#start-game {
  background-color: burlywood;
  width: 50%;
  height: 50%;
  margin: 100px auto 0 auto;
  box-sizing: border-box;
  padding: 10px;
}

#player-details {
  background-color: burlywood;
  width: 50%;
  height: 50%;
  margin: auto;
  box-sizing: border-box;
  padding: 10px;
}

#players {
  box-sizing: border-box;
  padding: 10px;
}

#sub-player {
  display: flex;
  box-sizing: border-box;
  padding: 10px;
  justify-content: space-between;
}

#players h2 {
  text-align: center;
}

#players button {
  display: block;
  margin: auto;
  box-sizing: border-box;
  padding: 5px 10px 5px 10px;
}
</style>

<style>
body {
  background-color: whitesmoke;
}
</style>