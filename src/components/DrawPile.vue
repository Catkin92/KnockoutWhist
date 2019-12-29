<template lang="html">
  <div>
    <div v-for="card in player_hand.cards">
      <img :src="card.images.png">
    </div>
    <div v-for="card in computer_hand.cards">
      <img :src="card.images.png">
    </div>
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
</style>
