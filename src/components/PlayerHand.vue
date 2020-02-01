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
  methods: {
    playCard(card) {
      var cardValue;
      switch(card.value){
        case "1":
          cardValue = 1;
          break;
        case "2":
          cardValue = 2;
          break;
        case "3":
          cardValue = 3;
          break;
        case "4":
          cardValue = 4;
          break;
        case "5":
          cardValue = 5;
          break;
        case "6":
          cardValue = 6;
          break;
        case "7":
          cardValue = 7;
          break;
        case "8":
          cardValue = 8;
          break;
        case "9":
          cardValue = 9;
          break;
        case "10":
          cardValue = 10;
          break;
        case "JACK":
          cardValue = 11;
          break;
        case "QUEEN":
          cardValue = 12;
          break;
        case "KING":
          cardValue = 13;
          break;
        case "ACE":
          cardValue = 14;
      }
      console.log(cardValue);
      // eventBus.$emit("play-card", card);
      eventBus.$emit("computer-response", (cardValue, card.suit));
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
