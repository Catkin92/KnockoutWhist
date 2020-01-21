<template lang="html">
  <div>
    <img v-for="card in computer_hand" :src="card.images.png">
  </div>
</template>

<script>
import {eventBus} from "../main.js"

export default {
  name: "computer-hand",
  props: ["computer_hand"],
  methods: {
    playSecond(){
        const array = this.computer_hand.forEach(card => card.code);
        return array;
      }
  },
  mounted() {
    // eventBus.$on("play-card", (played_card) => {
    //   const array = this.computer_hand.forEach(card => card.code);
    //   console.log(array);
      // eventBus.$emit("computer-response", computer_card);
    
  }
}
</script>

<style lang="css" scoped>
</style>
