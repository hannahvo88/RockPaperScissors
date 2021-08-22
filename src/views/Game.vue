
<template>
  <div>
    <div id="warningMessage">
      <p v-if="this.CheckLoginToken === null">Please login to play the game. You are now being redirected to login page!</p>
    </div>
    
    <div v-if="this.CheckLoginToken !== null" >
      <h1>Rock Paper Scissors</h1>
      <h2>Let's see if you can beat the computer</h2>

      <ScoreBoard />
      <div id="play-area">
        <Player :moves="moves" />
        <Computer :moves="moves" />
      </div>
        <h2 v-if="result" id="result">{{ result }}</h2>
    </div>
  </div>
</template>

<script>
import router from '../router';
import cookies from 'vue-cookies';
import ScoreBoard from "../components/ScoreBoard.vue";
import Player from "../components/Player.vue";
import Computer from "../components/Computer.vue";

export default {
  name: "Game",
  components: { 
    Player, 
    Computer, 
    ScoreBoard 
  },

  data() {
    return {
      result: "",
      moves: [
        { name: "Rock", image: "Rock.png" },
        { name: "Paper", image: "Paper.png" },
        { name: "Scissors", image: "Scissors.png" },
      ]
    };
  },
  computed: {
    playerChoice() {
      return this.$store.state.playerChoice;
    },
    computerChoice() {
      return this.$store.state.computerChoice;
    },
    CheckLoginToken() {
        return cookies.get('userToken');
    }
  },

  beforeMount() {
    if (this.CheckLoginToken === null) {
        setTimeout(() => {
            router.push('/');
        }, 3500);
    }
  },
  watch: {
    computerChoice: function(newChoice) {
      if (newChoice !== "") {
        this.result = "";
        let player = this.playerChoice;
        let computer = this.computerChoice;
        if (player === computer) {
          setTimeout(() => {
            this.result = "It's a tie";
          }, 400);
        } else if (
          (player == "Rock" && computer == "Scissors") ||
          (player == "Paper" && computer == "Rock") ||
          (player == "Scissors" && computer == "Paper") 
        ) {
          setTimeout(() => {
            this.result = "You Win!";
            this.$store.commit("incrementScore", "player");
          }, 400);
        } else {
          setTimeout(() => {
            this.result = "Computer Wins!";
            this.$store.commit("incrementScore", "computer");
          }, 400);
        }
      }
    },
    result: function() {
      if (this.result !== "") {
        setTimeout(() => {
          this.$store.commit("setComputerMove", "");
          this.result = "";
        }, 1200);
      }
    }
  }
};
</script>

<style scoped>
#result {
  font-size: 3.1em;
  color: white;
}
#play-area {
  display: flex;
  justify-content: center;
}
#warningMessage p{
    color: red;
    font-size: 2em;
}
</style>