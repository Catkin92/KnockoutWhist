# Knockout Whist (work in progress)
I started this project based on the card game Knockout Whist in late December as a way to explore game logic. The game is trick based, with one fewer cards being handed out each round.
I'm using https://deckofcardsapi.com/ for the deck, writing in Javascript using Vue as a framework.

# Notes On Progression

### 1st Feb 2020

#### Achieved
Fixed card evaluation, computer now plays legal cards in response to player, correct card gets taken out of its hand and the winner of each trick is correctly counted.

#### Next Steps
- Add in trump suit and change computer response and trick counter to reflect trumps inclusion in game
- Be able to switch player order so that if the computer wins a trick it plays first next time
- Be able to start second round with one fewer card each (if both players have won at least one trick)

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
