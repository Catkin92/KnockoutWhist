<template lang="html">
  <div>
    <img v-for="card in player_hand" @click="playCard(card)" :src="card.images.png">
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "player-hand",
  props: ["player_hand"],
  data() {
    return {
      card_value: null
    }
  },
  methods: {
    playCard(card) {
      switch(card.value){
        case "JACK":
          this.card_value = 11;
          break;
        case "QUEEN":
          this.card_value = 12;
          break;
        case "KING":
          this.card_value = 13;
          break;
        case "ACE":
          this.card_value = 14;
          break;
        default:
          this.card_value = parseInt(card.value)
      }
      eventBus.$emit("play-card", card);
      eventBus.$emit("computer-plays", this.card_value, card.suit);
    }
  }
};
</script>

<style lang="css" scoped>
div {
  display: flex;
}

li:hover {
  position: relative;
  top: -2vh;
}
</style>
