<template lang="html">
  <div>
    <img v-for="card in computer_hand.cards" :src="card.images.png">
  </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "computer-hand",
  props: ["computer_hand"]
}
</script>

<style lang="css" scoped>
</style>
