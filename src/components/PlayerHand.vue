<template lang="html">
  <div>
    <img v-for="card in player_hand.cards" @click="playCard(card)" :src="card.images.png">
  </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "player-hand",
  props: ["player_hand"],
  methods: {
    playCard(card){
      eventBus.$emit("play-card", (card))
    }
  }
}
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
