<template>

  <div class="container">
    <div class="game-status">
      <div class="game-level">
        <span>Level {{ levelNo+1 }}</span>
      </div>
      <div class="game-score">
        <span>124</span>
      </div>
    </div>
        <div class="game-wrapper">
          <div class="game">
            <template v-for="(item,index) in createCards" :key="index">
              <div class="card-wrap" :data-title="getImgTitle(item)" ref="card_wrap" :style="[setflexBasis,cardHeight]">
                <div class="card">
                  <div class="card-face card-front-face"  @click="flipCard" >
                    <img :src="front_face_img" alt="" >
                  </div>
                  <div class="card-face card-back-face">
                    <img :src="getImgUrl(item)" />
                  </div>
                </div>
              </div>
            </template>


          </div>
        </div>
      </div>

</template>

<script>
import levels from '@/assets/json/levels.json'

export default {
  name: 'App',
 data(){
    return{
      status:false,
      front_face_img:null,
      baseUrl:process.env.VUE_APP_BASE_URL,
      levels:[],
      levelNo:0,
      firstCard:null,
      secondCard:null,
      lockStatus:false,
      cardHeight:null,
    }
 },
  created() {
    this.levels=levels
    this.front_face_img=this.getImgUrl("information.svg");
    console.log()

  },
  mounted() {
    this.setCardHeight();
  },
  watch: {
    levelNo: function () {
      this.setCardHeight();
    },
  },
  computed:{
    createCards(){
      let cards=[];
      while (cards.length!==this.getCardCount){
        let index = Math.floor(Math.random() * this.getImgCount);
        let img=this.levels[this.levelNo].img[index];
        let count = cards.filter(item => item === img).length;
        if (count<2){
          cards.push(this.levels[this.levelNo].img[index]);
        }
      }
      return cards
    },
    setflexBasis(){
      return {'flex-basis':'calc('+this.levels[this.levelNo].flexBasis+'% - 1rem)'}
    },
    getImgCount(){
      return this.levels[this.levelNo].img.length;
    },
    getCardCount(){
      let row=this.levels[this.levelNo].row;
      let col=this.levels[this.levelNo].col;
      return row*col;
    }
  },
  methods:{
    setCardHeight(){
      let height=this.$refs.card_wrap.offsetWidth;
      height = height>100 ? 100 : height;
      this.cardHeight='height:'+height+'px';
    },
    getImgTitle(pic){
      return pic.split('/').reverse()[0];
    },
    getImgUrl(pic) {
      return require(`./assets/img/${pic}`)
    },
    checkCardsMatch(){
      if (!(this.firstCard && this.secondCard)) return ;
      return this.firstCard.title==this.secondCard.title ? true : false;
    },
    unflipCards(){
      setTimeout(()=>{
        this.firstCard.card.classList.remove('is-flipped')
        this.secondCard.card.classList.remove('is-flipped')
        this.resetCards()
      },1500)
    },
    selectCard(item){
      if (this.firstCard===null){
        this.firstCard={
          'card':item,
          'title':item.parentNode.getAttribute('data-title')
        };
        return
      }
      this.secondCard={
        'card':item,
        'title':item.parentNode.getAttribute('data-title')
      };
    },
    isSelectedCards(){
      if(this.firstCard && this.secondCard){
        this.lockStatus=true
        return true;
      }
      this.lockStatus=false
      return false;
    },
    resetCards(){
      this.firstCard=null;
      this.secondCard=null;
      this.lockStatus=false
    },
    increaseLevel(){
      if(this.levelNo<this.levels.length-1){
        this.levelNo++;
      }else{
        console.log("game completed.")
      }
    },
    flipCard(event){
      if (this.lockStatus) return ;
        let item=event.target.parentNode.parentNode;
        item.classList.add('is-flipped')
        this.selectCard(item)
        if (!this.isSelectedCards()) return ;

        if (this.checkCardsMatch()){
          this.resetCards()
        }else{
          this.unflipCards()
        }
    },
  }
}
</script>

<style lang='scss'>
@import 'assets/scss/style';
</style>