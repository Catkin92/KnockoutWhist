<template>
  <div>
    <draw-pile :deck="deck" :player_hand="player_hand" :computer_hand="computer_hand"></draw-pile>
  </div>
</template>

<script>
import DrawPile from "./components/DrawPile.vue"

export default {
  name: "app",
  components: {
    "draw-pile": DrawPile
  },
  data(){
    return{
      deck: [],
      player_hand: [],
      computer_hand: []
    }
  },
  mounted(){
    fetch("https://deckofcardsapi.com/api/deck/rbobbhmjlf7z/shuffle/")
    .then(res => res.json())
    .then(data => this.deck = data)

    fetch("https://deckofcardsapi.com/api/deck/rbobbhmjlf7z/draw/?count=7")
    .then(res => res.json())
    .then(data => this.player_hand = data)

    fetch("https://deckofcardsapi.com/api/deck/rbobbhmjlf7z/draw/?count=7")
    .then(res => res.json())
    .then(data => this.computer_hand = data)
  }
}

</script>

<style>

</style>
