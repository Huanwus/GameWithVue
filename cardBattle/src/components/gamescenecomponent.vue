<template>
  <div id="game-scene" :class="{'scene in': show,
              'scene out': !show}">
     <a href="#" id="scene-btn" class="button" @click="showGameOverScene()"></a>
  </div>
</template>

<script>
  import Constant from './constant'
  export default {
    data () {
      return {
        show: false,
        userWon: true
      }
    },
    mounted () {
      Constant.Event.$on(Constant.MSG_START_SCENE, function () {
        this.show = true
      }.bind(this))
    },
    methods: {
      showGameOverScene () {
        Constant.Event.$emit(Constant.MSG_OVER_GAME_SCENE, this.userWon)
      }
    }
  }
</script>

<style scoped>
  #game-scene {
    background: url(../../static/images/battle-bg.png) no-repeat;
  }
  .button {
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
  }
</style>
