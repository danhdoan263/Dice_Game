<template>
  <div id="app">
    <div class="wrapper clearfix">
      <!-- Player -->
      <comp-players
        v-bind:scorePlayers="scorePlayers"
        v-bind:activePlayers="activePlayers"
        v-bind:currentScore="currentScore"
      ></comp-players>
      <!-- Button -->
      <compButton
        v-bind:finalScore="finalScore"
        v-on:handleChangeFinalScore="handleChangeFinalScore"
        v-on:handleNewGame="handleNewGame"
        v-on:handleRollDices="handleRollDices"
        v-on:handleHoldScore="handleHoldScore"
      ></compButton>
      <!-- Dices -->
      <comp-dices
        v-bind:dices="dices"
        v-on:handleHoldScore="handleHoldScore"
      ></comp-dices>
      <!-- POPUP -->
      <compPopup
        v-on:handleClosePopup="handleClosePopup"
        v-bind:isOpenPopup="isOpenPopup"
      ></compPopup>
    </div>
  </div>
</template>

<script>
import compDices from "./components/compDices.vue";
import compPlayers from "./components/compPlayers.vue";
import compButton from "./components/compButton.vue";
import compPopup from "./components/compPopup.vue";
export default {
  name: "App",
  components: {
    compPlayers,
    compDices,
    compButton,
    compPopup,
  },
  data() {
    return {
      isPlay: false,
      activePlayers: 0,
      scorePlayers: [20, 30],
      currentScore: 0,
      isOpenPopup: false,
      dices: [4, 2],
      finalScore: 0,
    };
  },
  methods: {
    handleChangeFinalScore(e){
      this.finalScore = parseInt(e.target.value);
      console.log('final score from app.vue', this.finalScore);
    },
    handleHoldScore() {
      let oldScorePlayer = this.scorePlayers[this.activePlayers];
      this.scorePlayers[this.activePlayers] =
        this.currentScore + oldScorePlayer;
      this.activePlayers = this.activePlayers == 0 ? 1 : 0;
      this.currentScore = 0;
    },
    handleRollDices() {
      const dice1 = Math.floor(Math.random() * 6) + 1;
      const dice2 = Math.floor(Math.random() * 6) + 1;
      this.dices = [dice1, dice2];
      console.log(dice1, dice2);
      if (dice1 === 1 || dice2 === 1) {
        this.activePlayers = this.activePlayers == 0 ? 1 : 0;
      }
      this.currentScore = this.currentScore + dice1 + dice2;
    },
    handleNewGame(playGame) {
      if (playGame) {
        this.isOpenPopup = true;
      }
    },
    handleClosePopup() {
      (this.isOpenPopup = false),
        (this.isPlay = true),
        (this.activePlayers = 0),
        (this.scorePlayers = [0, 0]),
        (this.currentScore = 0);
      this.dices = [1, 1];
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url("./assets/back.jpg");
  background-size: cover;
  background-position: center;
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
