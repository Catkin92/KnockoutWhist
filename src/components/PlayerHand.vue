<template lang="html">
  <div>
    <li><img :src="card.images.png"></li>
  </div>
</template>

<script>
export default {
  name: "player-hand",
  props: ["card"]
}
</script>

<style lang="css" scoped>

li:hover {
  position: relative;
  top: -2vh;
}
</style>
