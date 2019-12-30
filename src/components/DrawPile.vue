<template lang="html">
  <div>
    <button @click="newGame">New Game</button>
    <h1>Computer</h1>
    <ul id="computer-hand">
      <computer-hand v-for="card in computer_hand.cards" :card="card"></computer-hand>
    </ul>
    <br>
    <br>
    <br>
      <img :src="played_card.image">
    <br>
    <br>
    <br>
    <br>
    <ul id="player-hand">
      <player-hand v-for="card in player_hand.cards" :card="card"></player-hand>
    </ul>
    <h1>Player</h1>
  </div>
</template>

<script>
import {eventBus} from "../main.js"
import PlayerHand from "./PlayerHand.vue"
import ComputerHand from "./ComputerHand.vue"

export default {
  name: "draw-pile",
  props: ["deck", "player_hand", "computer_hand", "played_card"],
  components: {
    "player-hand": PlayerHand,
    "computer-hand": ComputerHand
  },

  methods: {
    newGame(){
      eventBus.$emit('draw-cards', 7);
    }
  },
  mounted() {

  }
}
</script>

<style lang="css" scoped>

  ul {
    list-style: none;
    display: grid;
    grid-template-columns: repeat(7, 1fr);
  }

</style>
