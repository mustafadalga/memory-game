<template>
<div class="modal">
  <div class="modal-content">
    <div class="modal-header">
      <h1 class="modal-title" v-if="levelLength===levelNo">Game Completed</h1>
      <h1 class="modal-title" v-else>Level Completed</h1>
      <div class="close" @click="close">&times;</div>
    </div>
    <div class="modal-body">
      <template v-if="levelLength===levelNo">
        <h2>Congratulations!</h2>
        <p  >You passed all the levels and successfully completed the game.</p>
      </template>
      <template v-else>
        <h4>Congratulations!</h4>
        <p>You have successfully completed level {{  levelNo+1 }}.</p>
      </template>

      <div class="game-status">
        <div class="game-level">
          <h5>Level</h5>
          <span class="border-violet">{{ levelNo+1 }}</span>
        </div>
        <div class="game-score">
          <h5>Score</h5>
          <span class="border-violet">{{ score }}</span>
        </div>
      </div>

    </div>
    <div class="modal-footer">
      <button  v-if="levelLength===levelNo" class="btn" @click="restartGame">Play again <span class="btn-arrow">➔</span></button>
      <button  v-else class="btn" @click="nextLevel">Next Level <span class="btn-arrow">➔</span></button>

    </div>
  </div>
</div>
</template>

<script>
export default {
  name: "Modal",
  props:['levelNo','levelLength','score'],
  methods:{
    close(){
      // eslint-disable-next-line vue/custom-event-name-casing
      this.$emit('modalToggle');
    },
    nextLevel(){
      // eslint-disable-next-line vue/custom-event-name-casing
      this.$emit('increaseLevel');
    },
    restartGame(){
      // eslint-disable-next-line vue/custom-event-name-casing
      this.$emit('restartGame');
    }
  }

}
</script>
