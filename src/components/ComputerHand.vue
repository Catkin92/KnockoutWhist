<template lang="html">
  <div>
    <li><img :src="card.images.png"></li>
    <p>{{played_card}}</p>
  </div>
</template>

<script>

export default {
  name: "computer-hand",
  props: ["card", "played_card"],
  computed: {
    playSecond(){
      console.log(this.played_card)
    }
  },
  mounted(){

  }
}
</script>

<style lang="css" scoped>
</style>
