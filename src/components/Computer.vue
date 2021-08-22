
<template>
  <div id="computer" class="container">
    <h2>Computer</h2>
    <h3 v-if="computerChoice">Computer Chooses: </h3>
    <h3 v-else>Computer is calculating...</h3>
    <div class="selection" v-if="showCompChoice" key="chosen">
      <img class="move-img" :src="require('../assets/' + image)" alt="Image">
    </div>
  </div>
</template>

<script>
export default {
  name: "Computer",
  props: ["moves"],
  data() {
    return {
      image: "",
      showCompChoice: false
    };
  },
  computed: {
    computerChoice() {
      return this.$store.state.computerChoice;
    }
  },
  watch: {
    computerChoice: function(choice) {
      this.showCompChoice = false;
      let move = this.moves.find(move => move.name === choice);

      if(move) {
        // console.log("this.image /////--->", choice);
        this.image = move.image;
      }

      setTimeout(() => {
        this.showCompChoice = true;
      }, 300);
    }
  }
};
</script>