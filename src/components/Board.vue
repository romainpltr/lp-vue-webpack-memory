<template>
  <div class="board">
      <Card v-for="card in board" v-model="nCard" :key="card" v-on:selectedCard="selectedCard" :class="{ 'flipped': card.isFlipped, 'matched' : card.isMatched }" @click="flipCard(card)" :value="card.value" :img="card.img"></Card>
      <div v-if="finish" style="text-align: center; width:100px">
        Bravo !
      </div>
  </div>
</template>

<script>
import Card from '@/components/Card.vue'
import lodash from 'lodash'
export default {
  name: 'Board',
  created (){
    this.cards.forEach((card) => {
        
    });
    for(let i = 1; i <= this.nCard; i++){
      let id = Math.floor(Math.random() * (255 - 0));
      this.cards.push({
        img: 'https://picsum.photos/200/?image=' + id, 
        value: id,
        isFlipped: false
      })
    }   

    this.cards.forEach(card => {
      let card1 = lodash.cloneDeep(card);
      let card2 = lodash.cloneDeep(card1);
      this.board = this.board.concat(card1, card2);
    });

    this.board = lodash.shuffle(this.board);
  },
  data () {
    return {
      board: [],
      nCard: 8,
      cards: [],
      flippedCards: [],
      finish: false
    }
  },
  emits: ['selectedCard'],
  methods: {
    randomItem (items) {
      return items[Math.floor(Math.random()*items.length)];
    },

    flipCard(card){
      if(card.isFlipped === false){
        card.isFlipped = true;

        if(this.flippedCards.length < 2){
            this.flippedCards.push(card);
        }

        if(this.flippedCards.length === 2){
           this._match(card);
        } 
      }
    },

    _match(card){
        if(this.flippedCards[0].value === this.flippedCards[1].value){
            this.flippedCards.forEach(card => card.isMatched = true);
            
            if(this.board.every(card => card.isMatched === true)){
                this.finish = true;
            }

            this.flippedCards = [];
        }
        else {
          this.flippedCards.forEach(card => card.isFlipped = false);
          this.flippedCards = [];     
        }
        
        this.flippedCards = [];
    },
  },
  components: {
    Card
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.board {
    display: grid;
    margin-top: 2%;
    margin-bottom: 2%;
    grid-template-columns: repeat(4, 1fr);
    grid-column-gap: 20px;
    grid-row-gap: 20px;
    align-content: center;
    justify-content: space-around;
    margin-left: 50%;
    margin-right: 50%;

}
.card {
    width: 100%;
    height: 100%;
    position: relative;
}

.matched{
   opacity: 0.3;
}
</style>
