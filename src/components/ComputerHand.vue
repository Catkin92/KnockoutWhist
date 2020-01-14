<template lang="html">
  <div>
    <li><img :src="card.images.png"></li>
  </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "computer-hand",
  props: ["card", "played_card"],
  computed: {
    playSecond(){
      // console.log(this.played_card)
    }
  },
  mounted(){
    eventBus.$on("play-card", (played_card) => {
      console.log(played_card)
    })
  }
}
</script>

<style lang="css" scoped>
</style>
