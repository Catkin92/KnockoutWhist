<template lang="html">
  <div>
    <button @click="newGame">New Game</button>
      <div id="game-board">
        <div id="computer-hand">
          <h1>Computer</h1>
          <ul>
          <computer-hand v-for="card in computer_hand.cards" :card="card"></computer-hand>
          </ul>
        </div>
      <div id="playing">
        <img :src="played_card.image">
      </div>
      <div id="player-hand">
        <ul>
          <player-hand v-for="card in player_hand.cards" :card="card"></player-hand>
        </ul>
        <h1>Player</h1>
      </div>
    </div>
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

  #game-board {
    display: grid;
    grid-template-columns: 1fr;
    grid-template-rows: 1fr 1fr 1fr;
  }

  #playing {
    align-self: center;
    margin-left: 3vw;
  }

  ul {
    list-style: none;
    display: grid;
    grid-template-columns: repeat(7, 1fr);
  }

</style>
