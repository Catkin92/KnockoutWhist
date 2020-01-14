<template lang="html">
  <div>
    <img v-for="card in computer_hand.cards" :src="card.images.png">
  </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "computer-hand",
  props: ["computer_hand"],
  computed: {
    // playSecond(played_card){
    //   console.log(played_card);
    // }
  },
  mounted(){
    eventBus.$on("play-card", (played_card) => {
      console.log(played_card);
    })
  }
}
</script>

<style lang="css" scoped>
</style>
