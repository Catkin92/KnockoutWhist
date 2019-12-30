<template lang="html">
  <div>
    <button @click="newGame">New Game</button>
    <h1>Computer</h1>
    <ul id="computer-hand">
      <li v-for="card in computer_hand.cards"><img :src="card.images.png"></li>
    </ul>
    <br>
    <br>
    <br>
    <div v-if="played_card">
      <img :src="played_card.image">
    </div>
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

export default {
  name: "draw-pile",
  props: ["deck", "player_hand", "computer_hand", "played_card"],
  components: {
    "player-hand": PlayerHand
  },
  // data(){
  //   return{
  //     played_card: []
  //   }
  // },
  methods: {
    newGame(){
      eventBus.$emit('draw-cards', 7);
      eventBus.$emit('draw-opponent-cards', 7)
    }
  },
  mounted() {
    // eventBus.$on('play-card', (picked_card) => {
    //   this.played_card = picked_card;
    //   console.log(this.player_hand.filter(card => {
    //     card.code !== picked_card.code
    //   }))
    // })
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
