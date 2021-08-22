
<template>
    <div id="scoreboard">
        <h3>Your Score: {{ playerScore }}</h3>
        <h3>Computer's Score: {{ computerScore }}</h3>
    </div>
   
</template>

<script>


export default {
  name: "ScoreBoard",

  computed: {
    playerScore() {
      return this.$store.state.player;
    },
    computerScore() {
      return this.$store.state.computer;
    }
  },
  
  
};
</script>

<style scoped>

#scoreboard {
  display: flex;
  color: white;
  justify-content: space-around;
  font-size: 1.7em;
}
</style>