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
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>

            <div class="card-wrap">
              <div class="card " :class="status ? 'is-flipped' : ''" @click="test">
                <div class="card-face card-front-face">
                  <img src="../src/assets/img/information.svg" alt="">
                </div>
                <div class="card-face card-back-face">
                  <img src="https://marina-ferreira.github.io/memory-game/img/js-badge.svg" alt="">
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

</template>

<script>

export default {
  name: 'App',
 data(){
    return{
      status:false,
    }
 },
  methods:{
    test(){
      this.status=!this.status
    }
  }
}
</script>

<style lang='scss' >
@import 'assets/scss/style';
</style>