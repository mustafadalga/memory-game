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
              <div class="card-wrap" :data-title="getImgTitle(item)">
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
      levelNo:8,
      firstCard:null,
      secondCard:null,
      lockStatus:false,
    }
 },
  created() {
    this.levels=levels
    this.front_face_img=this.getImgUrl("information.svg");
  },
  computed:{
    createCards(){
      let cards=[];
      let row=this.levels[this.levelNo].row;
      let col=this.levels[this.levelNo].col;
      let imgCount=this.levels[this.levelNo].img.length;
      while (cards.length!==row*col){
        let randomPos = Math.floor(Math.random() * imgCount);
        let img=this.levels[this.levelNo].img[randomPos];
        var count = cards.filter(item => item === img).length;
        if (count<2){
          cards.push(this.levels[this.levelNo].img[randomPos]);
        }
      }
      console.log(cards)
      return cards
    },
  },
  methods:{
    getImgTitle(pic){
      return pic.split('/').reverse()[0];
    },
    getImgUrl(pic) {
      return require(`./assets/img/${pic}`)
    },
    checkCardsMatch(){
      if (!(this.firstCard && this.secondCard)) return ;
      let status= this.firstCard.title==this.secondCard.title ? true : false;
      console.log(status)
      return status;
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
    flipCard(event){
      this.levelNo++;
      console.log(event)
/*      if (this.lockStatus) return ;
        let item=event.target.parentNode.parentNode;
        item.classList.add('is-flipped')
        this.selectCard(item)
        if (!this.isSelectedCards()) return ;

        if (this.checkCardsMatch()){
          this.resetCards()
        }else{
          this.unflipCards()
        }*/
    },
  }
}
</script>

<style lang='scss'>
@import 'assets/scss/style';
</style>