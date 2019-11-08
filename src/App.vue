<template>
  <div id="app">
    <div class="wrapper clearfix">
      <comp-players v-bind:players="players" v-bind:active="playerActive" />

      <comp-controls
        v-bind:isPlaying="isPlaying"
        v-bind:finalScore="finalScore"
        v-on:handleChangeFinalScore="handleChangeFinalScore"
        v-on:newGame="newGame"
        v-on:rollDice="rollDice"
        v-on:hold="hold"
      />

      <comp-dices v-bind:dices="dices" />
      <comp-popup-rule v-bind:isOpenPopup="isOpenPopup" v-on:handleConfirm="handleConfirm" />
    </div>
  </div>
</template>

<script>
import CompPlayers from "./components/CompPlayers";
import CompDices from "./components/CompDices";
import CompControls from "./components/CompControls";
import CompPopupRule from "./components/CompPopupRule";
export default {
  name: "app",
  data() {
    return {
      players: [
        {
          id: 1,
          name: "Player 1",
          currentScore: 0,
          realScore: 0
        },
        {
          id: 2,
          name: "Player 2",
          currentScore: 0,
          realScore: 0
        }
      ],
      dices: [{ name: "dice-1", value: 1 }, { name: "dice-2", value: 1 }],
      playerActive: 0,
      isPlaying: false,
      isOpenPopup: false,
      finalScore: 4
    };
  },
  components: {
    CompPlayers,
    CompDices,
    CompControls,
    CompPopupRule
  },
  methods: {
    newGame() {
      this.isOpenPopup = true;
      console.log("app");
    },
    handleConfirm() {
      this.isPlaying = true;
      this.isOpenPopup = false;
      this.playerActive = 0;
      this.players[0].realScore = 0;
      this.players[1].realScore = 0;
      this.dices[0].value = 1;
      this.dices[1].value = 1;
    },
    rollDice() {
      if (this.isPlaying) {
        var check = false;
        this.dices.forEach((element, index) => {
          element.value = Math.floor(Math.random() * 6) + 1;
          this.players[this.playerActive].currentScore += element.value;
          if (element.value == 1) {
            check = true;
          }
        });
        if (check) {
          this.players[this.playerActive].currentScore = 0;
          this.players[this.playerActive].realScore = 0;
          this.playerActive = this.playerActive == 0 ? 1 : 0;
        }
      } else {
        alert('please enter button New Game');
      }
    },
    hold() {
      if (this.isPlaying) {
      this.players[this.playerActive].realScore += this.players[this.playerActive].currentScore;
      this.players[this.playerActive].currentScore = 0;
      if(this.players[this.playerActive].realScore > this.finalScore) {
        this.players[this.playerActive].name = 'WINNER';
        this.isPlaying = false;
      } else {
      this.playerActive = this.playerActive == 0 ? 1 : 0;
      }
      } else {
        alert('please enter button New Game');
      }
    },
    handleChangeFinalScore(e){
      var number = parseInt(e.target.value);
      if(isNaN(number)) {
        this.finalScore = '';
      } else {
        this.finalScore = number;
      }
    }
  },
  computed: {}
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
    url("./../public/assets/back.jpg");
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
