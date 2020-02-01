<template lang="html">
  <div>
    <button @click="newGame">New Game</button>
      <div id="game-board">

        <div id="computer-hand">
            <h4>Tricks: {{computer_tricks}}</h4>
            <computer-hand :computer_hand="computer_hand"></computer-hand>
        </div>

        <div id="playing">
          <h4>Player card</h4>
          <img :src="played_card.image">
          <h4>Computer Card</h4>
          <img :src="computer_card.image">
        </div>

        <div id="player-hand">
          <h4>Tricks: {{player_tricks}}</h4>
          <player-hand :player_hand="player_hand"></player-hand>
        </div>

      </div>
  </div>
</template>

<script>
import { eventBus } from "../main.js";
import PlayerHand from "./PlayerHand.vue";
import ComputerHand from "./ComputerHand.vue";

export default {
  name: "game-table",
  props: [
    "deck",
    "player_hand",
    "computer_hand",
    "played_card",
    "computer_card",
    "player_tricks",
    "computer_tricks"
  ],
  components: {
    "player-hand": PlayerHand,
    "computer-hand": ComputerHand
  },

  methods: {
    newGame() {
      eventBus.$emit("draw-cards", 7);
    }
  }
};
</script>

<style lang="css" scoped>
#game-board {
  display: grid;
  grid-template-rows: 1fr 1fr 1fr;
}

#game-board > div {
  display: flex;
}

#playing {
  margin-left: 3vw;
  grid-row: 2 / 3;
}

#computer-hand {
  grid-row: 1 / 2;
  list-style: none;
  margin-bottom: 2vh;
}

#player-hand {
  grid-row: 3 / 4;
  list-style: none;
  margin-top: 2vh;
}
</style>
