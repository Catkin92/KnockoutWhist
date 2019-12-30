<template lang="html">
  <div>
    <li @click="playCard"><img :src="card.images.png"></li>
  </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "player-hand",
  props: ["card"],
  methods: {
    playCard(){
      eventBus.$emit("play-card", (this.card))
    }
  }
}
</script>

<style lang="css" scoped>

li:hover {
  position: relative;
  top: -2vh;
}
</style>
