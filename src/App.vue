<template>
  <div>
    <game-table :deck="deck" :player_hand="player_hand" :computer_hand="computer_hand" :played_card="played_card"></game-table>
  </div>
</template>

<script>
import GameTable from "./components/GameTable.vue"
import {eventBus} from "./main.js"

export default {
  name: "app",
  components: {
    "game-table": GameTable
  },
  data(){
    return{
      deck: [],
      player_hand: [],
      computer_hand: [],
      played_card: []
    }
  },
  mounted(){
    fetch("https://deckofcardsapi.com/api/deck/new/shuffle/")
    .then(res => res.json())
    .then(data => this.deck = data)

    // NEW GAME -- DRAW X CARDS EACH
    eventBus.$on('draw-cards', (draw_number) => {
      fetch("https://deckofcardsapi.com/api/deck/" + this.deck.deck_id +"/draw/?count=" + draw_number)
      .then(res => res.json())
      .then(data => this.player_hand = data)

      fetch("https://deckofcardsapi.com/api/deck/" + this.deck.deck_id +"/draw/?count=" + draw_number)
      .then(res => res.json())
      .then(data => this.computer_hand = data)

      this.played_card = []
    })

    // PICKED CARD PLAYED AND REMOVED FROM HAND
    eventBus.$on('play-card', (played_card) => {
      this.played_card = played_card;
      const cards = this.player_hand.cards;
      cards.splice(cards.indexOf(played_card), 1);
    })

  }
}

</script>

<style>

  body {
    background-color: green;
  }

</style>
