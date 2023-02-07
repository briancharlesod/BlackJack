<template>
  <container id="grid">
  <container id="cards">
   
    
  
    <div id="dealer">
      <div id="cardPond">
    <div v-for="card in dealer" v-bind:key="card.id">
  <img v-if="card.faceUp" v-bind:src="card.img"/>

  <img v-else src="../assets/back.png"/>
  </div>
      </div>
      
      
  </div>
  <p v-show="showHands" class="box">{{this.dealerValue}}</p>

  <div id="player">
<div id="cardPond">
  
  <div v-for="card in player" v-bind:key="card.id">
  <img v-bind:src="card.img"/>
  </div>
  </div>
  
  </div>
  <div v-show="showHands" class="box">{{this.playerValue}}</div>
  <div v-show="showActions">
  <button class="button" v-on:click="hitPlayer()">Hit</button>
  <button class="button is-primary" v-on:click="stand()">Stand</button>
  <button class="button" v-show="showDoubleDown" v-on:click="doubleDown()">Double Down</button>
  <button class="button" v-show="showSplit" v-on:click="splitFunction()">Split</button>
  </div>
  

  
  
  <div id="player2">
  <div id="cardPond">
    <div v-for="card in player2" v-bind:key="card.id">
    <img v-bind:src="card.img" />
    </div>

    </div>
    
  </div>
  <div v-show="isSplit">{{ this.playerValue2 }}</div>
  <div v-show="splitActions">
    <button class="button" v-on:click="hitPlayer2()">Hit</button>
  <button class="button is-primary" v-on:click="dealerAI(); this.splitActions = false">Stand</button>

  </div>
  
  </container>
  <container id="sideBar">
    <p class="box">Total:{{this.money}}  Bet:{{this.bet}}</p>

    <div class="box" v-show="showWin">{{this.winMessage}}</div>
    <div v-show="showPlayAgain">
  <button class="button" v-on:click="playAgain()">New Deal</button>
  </div>
<div v-show="showPlayAgain">
  <input class="input" v-model="bet" type="number"/>
</div>
  </container>
  </container>
</template>

<script>


export default {
data() {
  return {
    cards: [
    {
        value: 11,
        suit: 'S',
        name: 'A-S',
        img: require('@/assets/ace_of_spades.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 11,
        suit: 'C',
        name: 'A-C',
        img: require('@/assets/ace_of_clubs.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 11,
        suit: 'H',
        name: 'A-H',
        img: require('@/assets/ace_of_hearts.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 11,
        suit: 'D',
        name: 'A-D',
        img: require('@/assets/ace_of_diamonds.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 2,
        suit: 'C',
        name: '2-C',
        img: require('@/assets/2_of_clubs.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 2,
        suit: 'S',
        name: '2-S',
        img: require('@/assets/2_of_spades.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 2,
        suit: 'H',
        name: '2-H',
        img: require('@/assets/2_of_hearts.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 2,
        suit: 'D',
        name: '2-D',
        img: require('@/assets/2_of_diamonds.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },

      {
        value: 3,
        suit: 'H',
        name: '3-H',
        img: require('@/assets/3_of_hearts.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 3,
        suit: 'S',
        name: '3-S',
        img: require('@/assets/3_of_spades.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 3,
        suit: 'D',
        name: '3-D',
        img: require('@/assets/3_of_diamonds.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 3,
        suit: 'C',
        name: '3-C',
        img: require('@/assets/3_of_clubs.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 4,
        suit: 'C',
        name: '4-C',
        img: require('@/assets/4_of_clubs.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 4,
        suit: 'H',
        name: '4-H',
        img: require('@/assets/4_of_hearts.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 4,
        suit: 'S',
        name: '4-S',
        img: require('@/assets/4_of_spades.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 4,
        suit: 'D',
        name: '4-D',
        img: require('@/assets/4_of_diamonds.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 5,
        suit: 'S',
        name: '5-S',
        img: require('@/assets/5_of_spades.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 5,
        suit: 'C',
        name: '5-C',
        img: require('@/assets/5_of_clubs.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 5,
        suit: 'H',
        name: '5-H',
        img: require('@/assets/5_of_hearts.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 5,
        suit: 'D',
        name: '5-D',
        img: require('@/assets/5_of_diamonds.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },

      {
        value: 6,
        suit: 'S',
        name: '6-S',
        img: require('@/assets/6_of_spades.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 6,
        suit: 'C',
        name: '6-C',
        img: require('@/assets/6_of_clubs.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 6,
        suit: 'H',
        name: '6-H',
        img: require('@/assets/6_of_hearts.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 6,
        suit: 'D',
        name: '6-D',
        img: require('@/assets/6_of_diamonds.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 7,
        suit: 'S',
        name: '7-S',
        img: require('@/assets/5_of_spades.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 7,
        suit: 'C',
        name: '7-C',
        img: require('@/assets/7_of_clubs.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 7,
        suit: 'H',
        name: '7-H',
        img: require('@/assets/7_of_hearts.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 7,
        suit: 'D',
        name: '7-D',
        img: require('@/assets/7_of_diamonds.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 8,
        suit: 'S',
        name: '8-S',
        img: require('@/assets/8_of_spades.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 8,
        suit: 'C',
        name: '8-C',
        img: require('@/assets/8_of_clubs.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 8,
        suit: 'H',
        name: '8-H',
        img: require('@/assets/8_of_hearts.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 8,
        suit: 'D',
        name: '8-D',
        img: require('@/assets/8_of_diamonds.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 9,
        suit: 'S',
        name: '9-S',
        img: require('@/assets/9_of_spades.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 9,
        suit: 'C',
        name: '9-C',
        img: require('@/assets/9_of_clubs.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 9,
        suit: 'H',
        name: '9-H',
        img: require('@/assets/9_of_hearts.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 9,
        suit: 'D',
        name: '9-D',
        img: require('@/assets/9_of_diamonds.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'S',
        name: '10-S',
        img: require('@/assets/10_of_spades.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'C',
        name: '10-C',
        img: require('@/assets/10_of_clubs.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'H',
        name: '10-H',
        img: require('@/assets/10_of_hearts.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'D',
        name: '10-D',
        img: require('@/assets/10_of_diamonds.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'S',
        name: 'J-S',
        img: require('@/assets/jack_of_spades2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'C',
        name: 'J-C',
        img: require('@/assets/jack_of_clubs2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'H',
        name: 'J-H',
        img: require('@/assets/jack_of_hearts2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'D',
        name: 'J-D',
        img: require('@/assets/jack_of_diamonds2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'S',
        name: 'Q-S',
        img: require('@/assets/queen_of_spades2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'C',
        name: 'Q-C',
        img: require('@/assets/queen_of_clubs2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'H',
        name: 'Q-H',
        img: require('@/assets/queen_of_hearts2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'D',
        name: 'Q-D',
        img: require('@/assets/queen_of_diamonds2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'S',
        name: 'K-S',
        img: require('@/assets/king_of_spades2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'C',
        name: 'K-C',
        img: require('@/assets/king_of_clubs2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'H',
        name: 'K-H',
        img: require('@/assets/king_of_hearts2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
      {
        value: 10,
        suit: 'D',
        name: 'K-D',
        img: require('@/assets/king_of_diamonds2.png'),
        faceUp: true,
        back: require('@/assets/back.png')
      },
    ],
    player: [],
    player2: [],
    dealer: [],
    deck: [],
    tempDeck: [],
    isSplit: false,
    showHands: false,
    showActions: false,
    showPlayAgain: true,
    winMessage: '',
    showWin: false,
    showSplit: false,
    showDoubleDown: false,
    splitActions: false,
    tempString1: '',
    tempString2: '',
    bet: 10,
    money: 1000
  }
},
methods: {
  playAgain() {
    if (this.bet <= this.money && this.bet > 0) {
    this.clearHands();
    this.moreCardsChecker();
    this.showWin = false;
    this.showSplit = false;
    this.showPlayAgain = false;
    this.showHands = true;
    this.showActions = true;
    this.isSplit = false;
    this.firstDeal();
    } else {
      this.showWin = true;
      this.winMessage = "Insufficient Funds";
    }
  },

  stand() {
    if(this.isSplit) {
      this.showActions = false;
      this.splitActions = true;
    } else {
    this.showActions = false;
    this.dealerAI();
    }
  },

  hitPlayer() {
    this.player.push(this.deck.shift());
    if(this.isSplit) {
      if (this.playerValue > 21) {
        this.showActions = false;
        this.splitActions = true;
      }
    } else {
    if (this.playerValue > 21) {
      this.showActions = false;
      this.dealerAI();
    }
  }
    this.showDoubleDown = false;
    this.showSplit = false;
  },

  hitPlayer2() {
    this.player2.push(this.deck.shift());
    if (this.playerValue2 > 21) {
      this.splitActions = false;
      this.dealerAI();
    }
  },

  hitDealer() {
    this.dealer.push(this.deck.shift());
    
  },

  splitFunction() {
    this.showDoubleDown = false;
    this.player2.push(this.player.pop())
    this.isSplit = true;
    this.showSplit = false;
  },

  blackJackChecker() {
    var dealBJ = false;
    var playBJ = false;
    if(this.dealer[0].value == 11) {
      if (this.dealer[1].value == 10) {
        dealBJ = true;
      }
    }
    if (this.dealer[0].value == 10) {
      if (this.dealer[1].value == 11) {
        dealBJ = true;
      }
    }
    if (this.player[0].value == 11) {
      if(this.player[1].value == 10) {
        playBJ = true;
      }
    }
    if (this.player[0].value == 10) {
      if (this.player[1].value == 11) {
        playBJ = true
      }
    }
    if (playBJ == true && dealBJ == true) {
      this.dealerAI();
    } else if (playBJ == true) {
      this.showActions = false;
      this.dealer[0].faceUp = true;
      this.winMessage = 'Player BlackJack'
      this.showWin = true;
      this.money = this.money + (this.bet * 1.5);
      this.showPlayAgain = true;
    } else if (dealBJ == true) {
      this.showActions = false;
      this.dealer[0].faceUp = true;
      this.winMessage = 'Dealer BlackJack'
      this.showWin = true;
      this.money = this.money - this.bet;
      this.showPlayAgain = true;
    }

  },
  
  shuffle(array) {
    for (var i = array.length - 1; i > 0; i--) {
         var j = Math.floor(Math.random() * (i + 1));
         var temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
},
dealerAI() {
  
  this.dealer[0].faceUp = true;
  while(this.dealerValue < 17) {
    this.hitDealer()
  }
this.winDetector();
},

winDetector() {
  if (this.isSplit) {
    if (this.playerValue > 21) {
  this.tempString1 = 'Dealer Wins Hand 1';
  this.money = this.money - this.bet;
  } else if (this.dealerValue > 21) {
  this.tempString1 = 'Player Wins Hand 1,';
  this.money = this.money + this.bet;
  } else if (this.playerValue > this.dealerValue) {
  this.tempString1 = 'Player Wins Hand 1,';
  this.money = this.money + this.bet;
  } else if (this.playerValue < this.dealerValue) {
  this.tempString1 = 'Dealer Wins Hand 1,';
  this.money = this.money - this.bet;
  } else {
  this.tempString1 = 'Hand 1 Push,'
  }
  if (this.playerValue2 > 21) {
  this.tempString2 = 'Dealer Wins Hand 2';
  this.money = this.money - this.bet;
} else if (this.dealerValue > 21) {
  this.tempString2 = 'Player Wins Hand 2';
  this.money = this.money + this.bet;
} else if (this.playerValue2 > this.dealerValue) {
  this.tempString2 = 'Player Wins Hand 2';
  this.money = this.money + this.bet;
} else if (this.playerValue2 < this.dealerValue) {
  this.tempString2 = 'Dealer Wins Hand 2';
  this.money = this.money - this.bet;
} else {
  this.tempString2 = 'Hand 2 Push'
}
if(this.tempString1 == 'Hand 1 Push,' && this.tempString2 == 'Hand 2 Push') {
  this.winMessage = 'Push'
} else {
  this.winMessage = this.tempString1 + ' ' + this.tempString2;
}
this.showWin = true;
this.showPlayAgain = true;


} else {

    if (this.playerValue > 21) {
  this.winMessage = 'Player Busts Dealer Wins';
  this.money = this.money - this.bet;
} else if (this.dealerValue > 21) {
  this.winMessage = 'Dealer Busts Player Wins';
  this.money = this.money + this.bet;
} else if (this.playerValue > this.dealerValue) {
  this.winMessage = 'Player Wins';
  this.money = this.money + this.bet;
} else if (this.playerValue < this.dealerValue) {
  this.winMessage = 'Dealer Wins';
  this.money = this.money - this.bet;
} else {
  this.winMessage = 'Push'
}
this.showWin = true;
this.showPlayAgain = true;
  }
},

clearHands() {
this.player = [];
this.dealer = [];
this.player2 = [];
},

doubleDown() {
  this.bet = this.bet + this.bet;
  this.player.push(this.deck.shift());
      this.showActions = false;
      this.dealerAI();
      this.bet = this.bet / 2;
    
},

firstDeal() {
this.hitPlayer();
this.hitDealer();
this.dealer[0].faceUp = false;
this.hitPlayer();
this.hitDealer();
if (this.player[0].value == this.player[1].value) {
    this.showSplit = true;
}
this.showDoubleDown = true;
this.blackJackChecker();
},

flipCard(card) {
  card.faceUp = !card.faceUp;
},

moreCardsChecker() {
  if(this.newDecks == true) {
    this.tempDeck = [];
    this.tempDeck = this.cards.slice(0);
    this.shuffle(this.tempDeck);
    this.deck = this.deck.concat(this.tempDeck);
    
  }
}

},
created() {
  this.deck = this.cards.slice(0);
  this.shuffle(this.deck);
},
computed: {
 
  newDecks() {
    if (this.deck.length < 15) {
      return true;
    } else {
      return false;
    }
  },
  
  playerValue() {
    var val = 0
    this.player.forEach(e => {
      if (e.faceUp) {
      val = val + e.value
      }
    })
    if (val > 21) {
      this.player.forEach(e => {
        
        if (e.faceUp) {
        if (e.value == 11) {
          e.value = 1;
          
        }}
      
      })
      val = 0
      this.player.forEach(e => {
        if(e.faceUp) {
      val = val + e.value
    }})
      
    }

    return val;
  },
  playerValue2() {
    var val = 0
    this.player2.forEach(e => {
      if (e.faceUp) {
      val = val + e.value
      }
    })
    if (val > 21) {
      this.player2.forEach(e => {
        
        if (e.faceUp) {
        if (e.value == 11) {
          e.value = 1;
          
        }}
      
      })
      val = 0
      this.player2.forEach(e => {
        if(e.faceUp) {
      val = val + e.value
    }})
      
    }

    return val;
  },
  dealerValue() {
    var val = 0
    this.dealer.forEach(e => {
      if (e.faceUp) {
      val = val + e.value
      }
    })
    if (val > 21) {
      this.dealer.forEach(e => {
        
        if (e.faceUp) {
        if (e.value == 11) {
          e.value = 1;
          
        }}
      
      })
      val = 0
      this.dealer.forEach(e => {
        if(e.faceUp) {
      val = val + e.value
    }})
      
    }

    return val;
  }
}
}

</script>

<style>
img {
  height: 200px;
  width: 150px;
}


div#cardPond {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
container#cards {
  display: flex;
  flex-direction: column;
  
  align-items: center;
}
html {
  background: url(../assets/redTop.jpg) no-repeat center center fixed;
  background-size: cover;
  height: 100%;
  
}
container#grid {
  padding: 30px;
  display: grid;
  grid-template-columns: 5fr 1fr;
  
  
}

</style>