<template>
  <div id="game-scene" :class="{'scene in': show,
              'scene out': !show}">
     <div class="card a" :class="{'flipped': cardAFlipped}">
       <div class="front face"></div>
       <div class="back face"></div>
     </div>

     <div class="card b" :class="{'flipped': cardBFlipped}">
       <div class="front face"></div>
       <div class="back face"></div>
     </div>
  </div>
</template>

<script>
  import Constant from './constant'
  export default {
    data () {
      return {
        show: false,
        userWon: true,
        cardAFlipped: false,
        cardBFlipped: false
      }
    },
    mounted () {
      Constant.Event.$on(Constant.MSG_START_SCENE, function () {
        this.show = true
        setTimeout(this.cardFlipped, 1000)
      }.bind(this))
    },
    methods: {
      cardFlipped () {
        this.cardAFlipped = true
        this.cardBFlipped = false
      },
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

  .card {
    width: 140px;
    height: 180px;
    perspective: 700;
    transition: all .5s ease-out;
  }

  .card > .face {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    border-radius: 4px;
    backface-visibility: hidden;
    transition: all 0.5s ease-out;
  }

  .card > .face.front {
    background: #81d1e9 url(../../static/images/front-face.png);
    transform: rotate3d(0, 1, 0, 0deg);
  }

  .card > .face.back {
    background: #4474b5 url(../../static/images/back-face-pattern.png);
    transform: rotate3d(0, 1, 0, 180deg);
    border: 3px solid white;
  }

  .card.flipped > .face.front {
    transform: rotate3d(0, 1, 0, -180deg);
  }

  .card.flipped > .face.back {
    transform: rotate3d(0, 1, 0, 0deg);
  }
</style>
