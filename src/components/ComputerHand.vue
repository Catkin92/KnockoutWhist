<template lang="html">
  <div>
    <img v-for="card in computer_hand" :src="card.images.png">
  </div>
</template>

<script>
import { eventBus } from "../main.js";

export default {
  name: "computer-hand",
  props: ["computer_hand"],
  mounted() {
   
  }
};
</script>

<style lang="css" scoped>
</style>
