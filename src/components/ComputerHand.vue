<template lang="html">
  <div>
    <li><img :src="card.images.png"></li>
  </div>
</template>

<script>
export default {
  name: "computer-hand",
  props: ["card"]
}
</script>

<style lang="css" scoped>
</style>
