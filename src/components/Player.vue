
<template>
  <div id="player" class="container">
    <h2>You</h2>
    <h3 v-if="showPlayerChoice">You Chose:</h3>
    <h3 v-else>Choose Your Move:</h3>
    <div v-if="showPlayerChoice" class="selection">
        <img class="move-img" :src="require('../assets/' + image)" alt="Image">
    </div>
      <div v-if="showmoves" id="moves">
        <button
          class="move-button"
          v-for="move in moves"
          :key="move.ID"
          @click="handleAttack(move.name)"
        >
          <a class="move-pic">{{ move.name }}</a> 
        </button>
      </div>
  </div>
</template>

<script>
export default {
  name: "Player",
  props: ["moves"],
  data() {
    return {
      showPlayerChoice: false,
      showmoves: true,
      image: ""
    };
  },
  methods: {
    handleAttack(choice) {
      let moves = ["Rock", "Paper", "Scissors"];
      let random = Math.floor(Math.random() * 3);
      this.$store.commit("setComputerMove", moves[random]);
      this.$store.commit("setPlayerMove", choice);
      let move = this.moves.find(move => move.name === choice);
      this.image = move.image;
      // console.log("previous image link---->", this.image)
      this.showmoves = false;
      setTimeout(() => {
        this.showPlayerChoice = true;
      }, 300);
    }
  },
  watch: {
    showPlayerChoice: function(visible) {
      if (visible) {
        setTimeout(() => {
          this.showPlayerChoice = false;
          this.showmoves = true;
        }, 1000);
      }
    }
  }
};
</script>

<style scoped>
#moves {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.move-button {
  background-color: green;
  color: white;
  border-radius: 15px;
  padding: 10px;
  margin: 5px;
  font-size: 1em;
  width: 50%;
  min-width: 110px;
  border: none;
}
.move-pic {
  font-size: 2em;
  padding-right: 10px;
}

</style>