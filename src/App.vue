<template>

  <div class="container">
    <div class="game-status">
      <div class="game-level">
        <span>1</span>
      </div>
      <div class="game-score">
        <span>124</span>
      </div>
    </div>
        <div class="game-wrapper">
          <div class="game">
            <template v-for="(item,index) in createCards" :key="index">
              <div class="card-wrap" :data-title="getImgTitle(item)" >
                <div class="card"  @click="test">
                  <div class="card-face card-front-face">
                    <img :src="front_face_img" alt="">
                  </div>
                  <div class="card-face card-back-face">
                    <img :src="getImgUrl(item)"/>
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
      levels:levels,
      levelNo:0,
      selectItems:[],
    }
 },
  created() {
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
    checkItemsMatch(){
      let status= this.selectItems[0]===this.selectItems[1] ? true : false;
      this.selectItems=[];
      return status;
    },
    test(event){
      let item=event.target.parentNode.parentNode;
      item.classList.toggle('is-flipped')
      let itemTitle=item.parentNode.getAttribute('data-title');
      this.selectItems.push(itemTitle);
      if (this.selectItems.length==2){
        console.log(this.checkItemsMatch())
      }
    },
  }
}
</script>

<style lang='scss'>
@import 'assets/scss/style';
</style>