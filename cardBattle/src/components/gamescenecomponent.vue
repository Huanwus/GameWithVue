<template>
  <div id="game-scene" :class="{'scene in': show,
              'scene out': !show}">
     <div class="card player a" :class="{'flipped': cardAFlipped,'out' : cardAOut, 'in': !cardAOut, 'selected': cardASelected}" @click="cardAClick()">
       <div class="front face"></div>
       <div class="back face"></div>
     </div>

     <div class="card player b" :class="{'flipped': cardBFlipped,'out' : cardBOut, 'in': !cardBOut, 'selected': cardBSelected}" @click="cardBClick()">
       <div class="front face"></div>
       <div class="back face"></div>
     </div>

     <div class="card player c" :class="{'flipped': cardCFlipped,'out' : cardCOut, 'in': !cardCOut, 'selected': cardCSelected}" @click="cardCClick()">
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
        cardBFlipped: false,
        cardCFlipped: false,
        cardAOut: true,
        cardBOut: true,
        cardCOut: true,
        cardASelected: false,
        cardBSelected: false,
        cardCSelected: false
      }
    },
    // 钩子函数监听管道里面有特定的消息的时候执行
    mounted () {
      Constant.Event.$on(Constant.MSG_START_SCENE, function () {
        this.show = true
        setTimeout(this.cardFlipped, 1000)
      }.bind(this))
    },
    methods: {
      cardFlipped () {
        this.cardAFlipped = true
        this.cardBFlipped = true
        this.cardCFlipped = true

        this.cardAOut = false
        this.cardBOut = false
        this.cardCOut = false
      },
      showGameOverScene () {
        Constant.Event.$emit(Constant.MSG_OVER_GAME_SCENE, this.userWon)
      },
      cardAClick () {
        this.cardASelected = true
        this.cardAFlipped = false
        this.cardBOut = true
        this.cardCOut = true
      },
      cardBClick () {
        this.cardBSelected = true
        this.cardBFlipped = false
        this.cardAOut = true
        this.cardCOut = true
      },
      cardCClick () {
        this.cardCSelected = true
        this.cardCFlipped = false
        this.cardBOut = true
        this.cardAOut = true
      }
    }
  }
</script>

<style scoped>
  #game-scene {
    background: url(../../static/images/battle-bg.png) no-repeat;
  }

  .card {
    position: absolute;
    width: 140px;
    height: 180px;
    perspective: 700;
    transition: all .5s ease-out;

    bottom: 170px;
  }

  .card.a {left: 15px;}
  .card.b {left: 170px;}
  .card.c {left: 325px;}

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

  .card.player.out {
    transform: translate3d(0, 180%, 0);
  }

  .card.player.in {
    transform: translate3d(0, 0, 0);
  }

  .card.player.flipped {
    cursor: pointer;
  }

  .card.player.in.flipped:hover {
    transform: translate3d(0, -10px, 0);
  }

  .card.selected {
    bottom: 250;
    left: 300px;
  }
</style>
