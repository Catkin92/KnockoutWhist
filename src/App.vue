<template>
  <div>
    <game-table
      :deck="deck"
      :player_hand="player_hand"
      :computer_hand="computer_hand"
      :played_card="played_card"
      :computer_card="computer_card"
      :player_tricks="player_tricks"
      :computer_tricks="computer_tricks"
    ></game-table>
  </div>
</template>

<script>
import GameTable from "./components/GameTable.vue";
import { eventBus } from "./main.js";

export default {
  name: "app",
  components: {
    "game-table": GameTable
  },
  data() {
    return {
      deck: [],
      player_hand: [],
      computer_hand: [],
      played_card: [],
      computer_card: [],
      computer_tricks: 0,
      player_tricks: 0
    };
  },
  methods: {
    getCardValue(card) {
      switch (card.value) {
        case "JACK":
          return 11;
          break;
        case "QUEEN":
          return 12;
          break;
        case "KING":
          return 13;
          break;
        case "ACE":
          return 14;
          break;
        default:
          return parseInt(card.value);
      }
    },
    removeComputerCard() {
      this.computer_hand.splice(this.computer_hand
        .indexOf(this.computer_card), 1);
    }
  },
  mounted() {
    fetch("https://deckofcardsapi.com/api/deck/new/shuffle/")
      .then(res => res.json())
      .then(data => (this.deck = data));

    // NEW GAME -- DRAW X CARDS EACH
    eventBus.$on("draw-cards", draw_number => {
      fetch(
        "https://deckofcardsapi.com/api/deck/" + this.deck.deck_id + "/draw/?count=" + draw_number)
        .then(res => res.json())
        .then(data => (this.player_hand = data.cards));

      fetch(
        "https://deckofcardsapi.com/api/deck/" + this.deck.deck_id + "/draw/?count=" + draw_number)
        .then(res => res.json())
        .then(data => (this.computer_hand = data.cards));

      this.played_card = [];
      this.computer_card = [];
      this.player_tricks = 0;
      this.computer_tricks = 0;
    });

    // PICKED CARD PLAYED AND REMOVED FROM HAND
    eventBus.$on("play-card", played_card => {
      this.played_card = played_card;
      const cards = this.player_hand;
      cards.splice(cards.indexOf(played_card), 1);
    });

    // COMPUTER REPONSE CARD PLAYED AND REMOVED FROM HAND
    eventBus.$on("computer-plays", (cardValue, suit) => {

      const playCard = card => {
        this.computer_card = card;
        this.removeComputerCard();
      };

      const sortedCompCards = this.computer_hand.sort((card1, card2) => {
        return this.getCardValue(card1) - this.getCardValue(card2);
      });

      const cardsOfSuit = sortedCompCards.filter(card => {
        return card.suit === suit;
      });

      const cardsOfSuitBeatsPlayer = cardsOfSuit.filter(card => {
        return this.getCardValue(card) > cardValue;
      });

      if (cardsOfSuitBeatsPlayer.length) {
        console.log("HIT");
        playCard(cardsOfSuitBeatsPlayer[0]);
        this.computer_tricks += 1;
      } else if (cardsOfSuit.length) {
        playCard(cardsOfSuit[0]);
        this.player_tricks += 1;
      } else {
        playCard(sortedCompCards[0]);
        this.player_tricks += 1;
      }

      // tries to find winning card of same suit
      // let response = this.computer_hand.find(card => {
      //   return this.getCardValue(card) > cardValue && card.suit === suit;
      // });
      //
      // // play card, discard card, and add to comp score
      // if (response) {
      //   this.computer_card = response;
      //   this.removeComputerCard();
      //   this.computer_tricks += 1;
      // } else {
      //   // find any card of the suit that will make do
      //   response = this.computer_hand.find(card => {
      //     return card.suit === suit;
      //   });
      //
      //   // if card of suit
      //   if (response) {
      //     // play card, discard card
      //     this.computer_card = response;
      //     this.removeComputerCard()
      //   }
      //   else {
      //     // otherwise pick the first one, play and discard
      //     this.computer_card = this.computer_hand[0];
      //     this.removeComputerCard()
      //   }
      //   // player wins this round
      //   this.player_tricks +=1;
      // }
    });
  }
};
</script>

<style>
body {
  background-color: green;
}
</style>
