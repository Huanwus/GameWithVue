<template>
  <div id="gameover-scene" :class="{'scene in': show,
                                    'scene out': !show,
                                    'won' : isWon,
                                    'loss': !isWon}">
   </div>
</template>

<script>
  import Constant from './constant'
  export default {
    data () {
      return {
        show: false,
        isWon: false
      }
    },
    mounted () {
      Constant.Event.$on(Constant.MSG_OVER_GAME_SCENE, function (userWon) {
        this.isWon = userWon
        this.show = true
      }.bind(this))
    }
  }
</script>

<style scoped>
  #gameover-scene.won {background:url(../../static/images/you-won.png) no-repeat;}
  #gameover-scene.loss {background:url(../../static/images/you-loss.png) no-repeat;}
</style>
