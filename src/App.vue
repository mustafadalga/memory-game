<template>

  <div class="container">
    <div class="game-status text-white">
      <div class="game-level">
        <h5>Level</h5>
        <span class="border-white">{{ levelNo+1 }}</span>
      </div>
      <div class="game-score">
        <h5>Score</h5>
        <span class="border-white">14500</span>
      </div>
    </div>
    <div class="game-wrapper">
          <div class="game">
            <template v-for="(item,index) in createCards" :key="index">
              <div class="card-wrap" :data-title="getImgTitle(item)" ref="card_wrap" :style="[setflexBasis,cardHeight]">
                <div class="card" :ref="'card' + index">
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
      <modal :level="levelNo" :score="score" @modalToggle="modalToggle" @increaseLevel="increaseLevel" :class="modalStatus ? 'open':''"></modal>
      </div>

</template>

<script>
import levels from '@/assets/json/levels.json'
import modal from "@/components/Modal";

export default {
  name: 'App',
  components:{
    modal
  },
 data(){
    return{
      status:false,
      front_face_img:null,
      levels:[],
      levelNo:0,
      score:0,
      firstCard:null,
      secondCard:null,
      lockStatus:false,
      cardHeight:null,
      flippedCartCount:0,
      modalStatus:false,
    }
 },
  created() {
    this.levels=levels
    this.front_face_img=this.getImgUrl("information.svg");
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
      return this.getImgCount*2;
    }
  },
  methods:{
    modalToggle(){
      this.modalStatus=!this.modalStatus
    },
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
    unflipAllCards(){
      for (let index=0;index<this.getCardCount;index++){
        this.$refs['card'+index].classList.remove('flip')
      }
    },
    unflipSelectedCards(){
      setTimeout(()=>{
        this.firstCard.card.classList.remove('flip')
        this.secondCard.card.classList.remove('flip')
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
        this.unflipAllCards();
        setTimeout(()=>{
          this.levelNo++
        },1500)
        console.log("sonraki seviye")
      }else{
        console.log("game completed.")
      }
    },
    isLevelCompleted(){
      if (this.flippedCartCount===this.getImgCount){
        this.increaseLevel()
      }
    },
    flipCard(event){
      if (this.lockStatus) return ;
      let item=event.target.parentNode.parentNode;
      if (this.firstCard && item===this.firstCard.card) return ;

      item.classList.add('flip')
      this.selectCard(item)

      if (!this.isSelectedCards()) return ;

        if (this.checkCardsMatch()){
          this.flippedCartCount++;
          this.isLevelCompleted()
          this.resetCards()
        }else{
          this.unflipSelectedCards()
        }
    },
  }
}
</script>

<style lang='scss'>
@import 'assets/scss/style';
</style>