<template lang="html">
  <div>
    <h1>Computer</h1>
    <ul id="computer-hand">
      <li v-for="card in computer_hand.cards"><img :src="card.images.png"></li>
    </ul>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <br>
    <ul id="player-hand">
      <li v-for="card in player_hand.cards"><img :src="card.images.png"></li>
    </ul>
    <h1>Player</h1>
  </div>
</template>

<script>
export default {
  name: "draw-pile",
  props: ["deck", "player_hand", "computer_hand"],
  mounted(){
    // fetch("https://deckofcardsapi.com/api/deck/" + deck_id + "/draw/")
  }
}
</script>

<style lang="css" scoped>

  ul {
    list-style: none;
    display: grid;
    grid-template-columns: repeat(7, 1fr);
  }

  #player-hand li:hover {
    position: relative;
    top: -2vh;
  }

</style>
